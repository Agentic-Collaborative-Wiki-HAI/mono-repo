# Agentic Collaborative Wiki

A shared knowledge base where an AI agent is a participant rather than a private assistant — and where everything it proposes goes through human review before it becomes part of the record.

Term project for **INF 385T.13 Human-AI Interaction**, UT Austin iSchool, Fall 2026.

## The problem

Agentic knowledge tools are getting good, but they are almost all **personal**. They assume you know Markdown, run Obsidian or VS Code, are comfortable in a terminal, and can drive a coding agent against local files. That rules out most people.

Meanwhile, mature wikis solved something those tools never attempted: **the social layer.** Revision history. Rollback. Proposed and contested edits. Discussion attached to a change. Identifiable contributors. Ways to handle a bad edit.

Put those together and you get the question this project is actually about:

> **What happens when an AI agent becomes an actor inside a shared, governed knowledge system rather than a private assistant working for one person?**

Not "a chatbot next to a wiki." The interesting part is governance — who reviews what the agent proposes, how they see what would change and why, and how that decision enters the record.

## Who it's for

**Small academic and research teams**, to start. Collaboration around accumulated knowledge is native to how they work, they are reachable for evaluation, and it keeps us honest about scope. We are not trying to solve collaborative knowledge management in general.

## What we're building first

The smallest thing that demonstrates the idea:

> A nontechnical member of a shared workspace asks an agent to work with shared knowledge. The agent reads and searches the corpus and produces a **transparent proposed change**. Another human can understand and review that proposal before it becomes part of the shared record.

The loop:

1. Agent reads and searches the shared corpus
2. Agent creates a **proposed** edit — never a silent one
3. Humans see what would change, and why
4. Humans accept, reject, or revise
5. Only accepted changes become canonical
6. The decision enters revision history

If that works well, the idea is demonstrated. Everything else is supporting infrastructure.

## Deliberately out of scope

Real-time multi-cursor collaboration · CRDTs · multi-agent orchestration · autonomous background agents · MediaWiki feature parity · elaborate permissions · federation · enterprise RAG infrastructure · local model hosting to save a few dollars.

This is a semester project. Scope discipline is the main risk.

## Open architecture questions

Nothing here is decided. These are the things the first spikes exist to answer.

- **Extend an existing wiki, or build small from scratch?** Wiki.js is the leading candidate for the first path; MediaWiki has a richer AI/MCP ecosystem but a heavier architecture.
- **Which model is good enough?** We want the *cheapest* model that reliably does the real tasks, not the most capable one. This is a benchmark question, not an opinion.
- **What agent harness, if any?** A thin vendor-neutral tool-calling loop keeps models swappable.
- **Where does it run**, and who owns the API keys and billing?

## Design commitments

Two things we are not planning to relitigate:

- **The model stays swappable.** No architecting around a single vendor.
- **The agent proposes; humans dispose.** Agent output creates reviewable proposals. It does not silently mutate shared knowledge. This is the whole point of the project.

## Repository layout

```text
docs/
  active-spikes/   current spike work — a concept doc plus a .todo.md each
  decisions/       durable architecture decisions, numbered
  scratch/         rough thinking, not authoritative
  archive/         closed or superseded spikes
skills/            agent workflows this repo carries
TODO.md            spike index and coordination map
AGENTS.md          instructions for AI agents working in this repo
```

## Getting started

Nothing to run yet — the stack is not chosen. See [TODO.md](TODO.md) for open spikes and pick one that interests you.

**If you are working with an AI agent in this repo, read [AGENTS.md](AGENTS.md) first.**

## How we work

**People pick up work rather than being assigned it.** Issues and the project board are the coordination surface; architecture decisions land in `docs/decisions/` so they survive the conversation that produced them.

A few words mean specific things here — **epic**, **spike**, **task** — and they are defined in [docs/decisions/0003](docs/decisions/0003-how-we-name-and-organize-work.md). The short version: an epic is an open-ended topic, a spike is a bounded chunk of work with its own docs, and a plain issue is just a piece of work someone owns.

## License

[AGPL-3.0](LICENSE). Chosen deliberately: if this becomes something people run as a service, the improvements should come back.
