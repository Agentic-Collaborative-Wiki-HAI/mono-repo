# 0001 Agent Proposes, Humans Dispose
## Context
Personal agentic knowledge tools let an agent write directly into the user's notes. That is acceptable when the knowledge base belongs to one person and only that person bears the cost of a bad edit.

A *shared* knowledge base is different. A wrong or unwanted edit propagates to everyone who relies on it, and the person who has to catch it is usually not the person who prompted the agent.

## Decision
**Agent output creates reviewable proposals. The agent does not silently mutate canonical shared knowledge.**

A proposal must show what would change and why. A human accepts, rejects, or revises it. Only accepted changes become canonical, and the decision enters revision history.

## Consequences
**Easier:** the project has a clear research question — how AI-proposed changes should be surfaced, reviewed, attributed, and incorporated. Review UI becomes the centerpiece rather than an afterthought.

**Harder:** every write path needs a proposal representation and a review surface. There is no shortcut where the agent just edits the page.

**Out of scope:** autonomous background agents that maintain the wiki without review. That is a different project.

## Links
- [README.md](../../README.md)
