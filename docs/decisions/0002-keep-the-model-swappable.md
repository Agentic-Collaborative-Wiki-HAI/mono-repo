# 0002 Keep The Model Swappable
## Context
It is tempting to build against one vendor's agent SDK and be done with it. Two problems: it locks the prototype to that vendor's pricing and availability, and it makes the cost question — *what is the cheapest model that is actually good enough?* — hard to answer, because comparison requires rewriting the integration.

The project has a small compute budget. Cost is an architecture constraint, not a later optimization.

## Decision
**Do not architect around a single model provider.** Candidates worth testing include OpenAI, Anthropic, Qwen, and DeepSeek.

A thin vendor-neutral tool-calling loop is preferred over a vendor agent SDK, because it makes model comparison cheap.

## Consequences
**Easier:** swapping models to compare cost and quality. Running the benchmark that answers cheapest-good-enough. Not being stranded if a provider changes pricing mid-semester.

**Harder:** we give up conveniences that vendor SDKs provide, and have to write more of the loop ourselves.

**Explicitly not implied:** this is not a commitment to local model hosting. Self-hosting to save a few dollars is out of scope.

## Links
- [README.md](../../README.md) · [TODO.md](../../TODO.md) — the agent/model spike
