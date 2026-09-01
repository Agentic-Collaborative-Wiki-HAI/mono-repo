# 0003 How We Name And Organize Work
## Context
This repo runs two systems that both track work, and without a stated boundary they compete.

**GitHub issues and the project board** are how people coordinate — who owns what, what is open, what is blocked. Visible without cloning anything.

**Spike docs in `docs/active-spikes/`** are how an agent keeps track of work in progress. A concept doc holds why the work exists and what was decided; a `.todo.md` holds granular state. They are far more detailed than an issue and are read mostly by agents, not people.

Both contain things called "tasks." Deciding which is authoritative, and at what resolution, is the actual question — the naming problem follows from it.

There is also a trap in the word *spike*. In XP it means a timeboxed throwaway investigation that returns an answer. **That is not what it means here**, and an earlier draft of this repo's docs defined it that way, which was wrong.

## Decision
**Four terms, at different resolutions.**

**Epic** — a GitHub issue type. A durable topic that accumulates work over time and stays open. *Design the interface.* An epic is a thin organizing shell; it has no natural end and may sit open while children close beneath it.

**Issue** — a piece of work someone owns and others need visibility into. **A plain issue is a task**, so there is no `Task` type — the type would only restate what the issue already is. Types exist for the two cases that carry real information: `Epic` and `Bug`.

**Spike** — a **bounded chunk of work carrying its own docs**: a concept doc plus a `.todo.md` in `docs/active-spikes/`. A spike produces real work, not throwaway code.

**task** — lowercase. A checkbox inside a spike's `.todo.md`. Never a GitHub object.

**Spikes end. Epics do not.** When related work comes around again, open a successor spike rather than reopening the original — `wcag-seo`, then `wcag-seo2`. The concept doc's whole value is that someone can read it and understand the shape of the work; reopening indefinitely makes it sprawl past the point of being followable.

**Issues and `.todo.md` files do not compete, because they are not at the same resolution.** An issue is a unit of human-visible ownership. A checkbox is a step. You do not file issues for checkboxes.

**Not every issue has a spike.** Design and research work performed in Figma or elsewhere is tracked here for visibility and co-location, with no repo docs behind it at all.

## Consequences
**Easier:** no argument about whether something is a spike or a task, because they are not alternatives — they are different resolutions. No duplicated task tracking. An agent reading a fresh clone finds the concept doc; a person reading the board finds the issue.

**Harder:** two places to look when reconstructing what happened. Mitigated by issues linking their spike doc and spike docs recording their issue number.

**Deliberately kept:** archived spikes are not deleted. They are how a future agent learns what was already tried and rejected.

**Out of scope:** unifying the two systems into one. They serve different readers at different resolutions, and collapsing them would make one of them worse.

## Links
- [AGENTS.md](../../AGENTS.md) · [TODO.md](../../TODO.md) · [skills/run-project-spike/SKILL.md](../../skills/run-project-spike/SKILL.md)
