# TODO
Spike index. Detailed state lives in each spike's `.todo.md`; this file stays scannable.

**GitHub Issues and the project board are the live work tracker for humans.** This file indexes the repo's spikes — bounded chunks of work that carry their own docs. See [AGENTS.md](AGENTS.md) for how the two relate.

## Active Spikes
None yet. The five below are proposed and unclaimed.

## Open Questions — Not Yet Spikes
These need answering. Most will become issues; the ones with real work behind them will get a spike doc pair in `docs/active-spikes/`.

**Agent / model.** Can a *cheap* model reliably search a small shared corpus, read documents, call tools, and propose a controlled edit without touching unrelated content? Test several cost tiers and providers. Track task success, failure mode, latency, tokens, and dollars. **The question is what is cheapest-good-enough, not what is best.**

**Existing wiki.** Can Wiki.js expose enough programmatic and UI extension surface to support agent-proposed edits without consuming the semester in framework-specific work? Specifically: read and search pages externally, write revisions programmatically, surface a proposal diff in the UI, extend the interface without fighting the framework.

**Greenfield / editor.** If the wiki route is worse, can Vue plus a Typora-like Markdown editor plus Supabase provide the basic collaborative UI cheaply? Milkdown/Crepe is a candidate.

**Interaction design.** What does an agent proposal actually look like to a reviewer? Diff, rationale, affected pages, confidence and uncertainty, accept/reject/modify, attribution, rollback. **This one needs no code and is the closest to the project's actual research question.**

**Deployment.** Smallest path to a shared prototype with server-side model credentials. Who owns the keys and billing.

## Waiting On A Human
- **Team membership** is not final until the Sept 4 course deadline.
- **Compute budget** — roughly $100 was indicated as possibly available. Not confirmed.

## Decisions Made
See `docs/decisions/`. In short: the model stays swappable, and **the agent proposes rather than silently mutating shared knowledge.**

## Course Milestones
- **Fri Sept 4, 1:00pm** — team formation and initial idea submission
- **Fri Sept 18, 1:00pm** — formal project proposal. **Requires a timeline with at least three milestones and named responsibilities**, so spike work between now and then should produce evidence for that plan.
