# Project Board Setup
The workflows in `.github/workflows/` drive the project board. They read the board's identifiers from **repository variables**, not hardcoded values, so nothing here needs editing when the board changes — you update the variables instead.

Set this up once. Everything after that is version-controlled.

## Board columns
The `Status` field should have these options, in this order:

`Backlog` · `Blocked` · `Upcoming` · `On Deck` · `Active` · `Done`

## What the workflows do
| Trigger | Effect |
|---|---|
| Issue opened | Added to the board in **Backlog** |
| Issue closed | Moved to **Done** |
| Issue reopened | Moved back to **Backlog** for re-triage |
| `blocked` label added | Moved to **Blocked** |
| `blocked` label removed | Moved to **On Deck** |
| Card dragged out of Done while the issue is closed | Issue **reopened** (timer, every 15 min) |
| Issue has open native blockers (`blocked by #N`) | Moved to **Blocked** (timer, every 15 min) |

**Nothing automates Upcoming or Active.** Those are human judgment about what is next and what is being worked on, and automating them would fight the person moving cards.

**Two paths into Blocked, deliberately.** Native issue dependencies handle "blocked by ticket #12"; the `blocked` label handles everything that is not a ticket — waiting on a person, a decision, a date. Dependencies are a *relationship*, not a status, so they do not move a card on their own; `board-reconcile.yaml` bridges that.

**Unblocking is not symmetric.** Clearing a dependency does not move a card out of Blocked, because the issue may still be held by the label. Removing the `blocked` label moves it to On Deck. Otherwise, move it by hand.

**The two timer-based reconciliations exist because GitHub has no event for them.** Board changes cannot trigger a repo workflow, GitHub ships auto-close but no auto-reopen, and dependency changes do not fire a usable event. `board-reconcile.yaml` supports `workflow_dispatch` with a dry-run input if you want to see what it would do before it does it.

## 1. Create the token
The workflows need a token that can write to org-level Projects. `GITHUB_TOKEN` cannot — it has no Projects scope.

**Fine-grained PAT** (preferred), at https://github.com/settings/personal-access-tokens/new:
- **Resource owner:** the `Agentic-Collaborative-Wiki-HAI` org, not your personal account
- **Repository access:** this repository
- **Repository permissions:** Issues → Read and write · Metadata → Read
- **Organization permissions:** **Projects → Read and write**

If you are not an org owner, the org must approve the token before it works.

**Classic PAT** also works: scopes `repo` and `project`.

Save it as a repository secret named **`ACTIONS_TOKEN`**:

```sh
gh secret set ACTIONS_TOKEN --repo Agentic-Collaborative-Wiki-HAI/mono-repo
```

## 2. Find the board's IDs
Get the project number from the org's Projects tab, then:

```sh
ORG=Agentic-Collaborative-Wiki-HAI
NUM=1   # your project number

# Project ID and every Status option ID in one shot
gh api graphql -f query='
  query($org: String!, $num: Int!) {
    organization(login: $org) {
      projectV2(number: $num) {
        id
        field(name: "Status") {
          ... on ProjectV2SingleSelectField {
            id
            options { id name }
          }
        }
      }
    }
  }' -F org="$ORG" -F num=$NUM
```

## 3. Store them as repository variables
```sh
R=Agentic-Collaborative-Wiki-HAI/mono-repo
gh variable set PROJECT_ID           --repo $R --body "PVT_..."
gh variable set STATUS_FIELD_ID      --repo $R --body "PVTSSF_..."
gh variable set BACKLOG_OPTION_ID    --repo $R --body "..."
gh variable set BLOCKED_OPTION_ID    --repo $R --body "..."
gh variable set ON_DECK_OPTION_ID    --repo $R --body "..."
gh variable set DONE_OPTION_ID       --repo $R --body "..."
```

Option IDs are the short hashes from the query above — they are not secret, which is why these are variables rather than secrets.

## 4. Test
Open a throwaway issue and confirm it lands in Backlog, then close it and confirm it moves to Done. Check the Actions tab if it does not.

## Why not the built-in Project workflows
GitHub's built-in workflows would do most of this without a token. They are not used here because **they live in the Project UI and cannot be version-controlled, reviewed, or reasoned about from the repo** — and their feature set runs out quickly. These workflows are worse to set up once and better to live with.
