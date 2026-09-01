# Agent Instructions
Instructions for AI agents working in this repository. Humans should read [README.md](README.md) first.

## What This Repo Is
The term project for INF 385T.13 Human-AI Interaction (UT Austin iSchool, Fall 2026): a collaborative knowledge base where an AI agent proposes changes that humans review before they enter the shared record.

**This is a shared student team repository, not one person's project.** Multiple people with different skill levels and different amounts of time will work here. Optimize for legibility to the next person, not for cleverness.

## Public Repository — Privacy Rules
This repo is public under AGPL-3.0. Everything committed here is visible to anyone.

- **Never commit API keys, tokens, or credentials.** Model provider keys are the specific risk on this project. Use `.env` locally and repository secrets in CI. `.gitignore` covers the common patterns, but it is a safety net, not a substitute for care.
- **Never commit classmates' personal information** — no phone numbers, home addresses, private messages, or anything from Canvas that is not already public.
- **Do not commit research participant data.** If user evaluation produces transcripts, notes, or recordings, they stay out of this repo. Consent and IRB questions are unresolved; ask before writing any participant data anywhere.
- Do not commit unreleased course material, other students' work, or anything from the instructor that was not shared publicly.

## Skills Are Repo Authority
`skills/` holds workflows this repo carries so it is self-contained after clone. **A repo-local skill overrides a global skill of the same name.** Global skills are fallback seed material.

Current local skills: `run-project-spike`, `commit-work`, `triage-project-misc`, `pin-issue`, `write-skills`, `draft-approval-slate`.

## Where Things Go
| Path | What belongs there |
|---|---|
| `docs/active-spikes/` | Current spike work — a concept doc and a `.todo.md` per spike |
| `docs/decisions/` | Durable architecture decisions, numbered `0001-title.md` |
| `docs/scratch/` | Rough thinking, references, early notes. Not authoritative |
| `docs/archive/` | Closed or superseded spikes. History, not current rules |
| `TODO.md` | The spike index and coordination map. Keep it scannable |
| `skills/` | Agent workflows |

**Do not create a `README.md` inside `docs/` or its subfolders.** `TODO.md` is the index; `ls` handles the rest.

## How Work Is Organized
**Spikes, not assigned roles.** A spike is a bounded investigation that retires a specific uncertainty — "can Wiki.js expose enough API surface to support agent-proposed edits?" — and produces evidence. People self-select the questions they want to answer.

This is deliberate. The team's actual technical capacity is not yet known, and small real work reveals it better than role labels assigned up front.

When an architecture question gets settled, write it into `docs/decisions/` so it survives the conversation that produced it.

## Working With The Team's Code
- **Do not force-push shared branches.** Do not rewrite history that others may have pulled.
- **Do not commit on someone's behalf** or amend their commits.
- If the worktree is dirty with changes you did not make, **stop and ask.** Someone else may be mid-task.
- Commit by explicit pathspec. Never `git add -A` in a shared repo — see `skills/commit-work/`.
- **Do not add `Co-Authored-By:` trailers.**

## Scope Discipline
This project is at real risk of being too large for one semester. The out-of-scope list in [README.md](README.md) is load-bearing.

**If a change requires real-time collaboration, CRDTs, multi-agent orchestration, or a permissions matrix, it is almost certainly out of scope.** Say so rather than building it.

The minimum vertical slice is in the README. Work that does not serve it needs a reason.

## Markdown And Prose Style
Do not hard-wrap prose in Markdown, comments, docs, or examples. Let editors handle soft wrapping. Preserve paragraphs as single lines unless line breaks carry meaning, such as lists, tables, code blocks, quoted text, frontmatter, or an existing semantic-line-break style.

Avoid reflow-only diffs. When editing prose, change the smallest relevant span instead of rewrapping neighboring paragraphs.

When touching existing Markdown or prose, apply this preferred style to the paragraph, section, or example being edited so files converge over time. Do not mass-reformat untouched sections just to normalize style unless asked for a cleanup pass.

Prefer compact Markdown heading spacing in hand-authored docs: do not add blank lines only to separate adjacent headings from each other. Follow existing file style, and let explicit project tooling win when a formatter or linter requires a different layout.

## Validation
No build or test tooling exists yet — the stack is not chosen. When it is, document how to validate changes here.

Until then: check that Markdown links resolve and that nothing secret is staged before committing.

## CLAUDE.md
`CLAUDE.md` is a symlink to this file. Edit `AGENTS.md`.
