# dark-factory

Design for a software factory that builds software with no human in the loop: opencode agents triage issues, implement, verify, review, merge and deploy autonomously. The owner writes issues and reads reports.

A *dark factory* is the end state of agentic software delivery — lights-out, no human gate between an issue and production. This repository holds the design: trust boundary, risk tiers, holdout scenarios, secrets and blast radius, merge and deploy guardrails, stop rules, self-modification limits and kill switch.

**Status:** design draft. Phase 0 (shadow mode) has not started. There is no code here yet.

## Why a separate project

The factory is not tied to any one application. The spec was drafted against a reference target, [`vinyl-session-page`](https://github.com/jirigrill/vinyl-session-page) — a small Go + SQLite web app on a single host — and that is where the first factory run will point. Everything application-specific in the spec (Go toolchain, Playwright, SQLite, a droplet, a YouTube API twin) is an example rather than a requirement.

## Contents

- [`docs/dark-factory-spec.md`](docs/dark-factory-spec.md) — the full design: numbered decisions, the per-issue pipeline, build-vs-buy analysis, open questions and references.

## Design in one page

- **Trust boundary:** full dark reached in phases. Phase 0 runs the whole pipeline but stops at an open PR; auto-merge is promoted per risk tier on measured owner agreement, and demoted on reverts.
- **Risk tiers:** low (docs, copy, additive UI) merges first; medium (ordinary features) next; high (migrations, auth, quota use, deploy code) always needs the owner.
- **Spec before code:** an ambiguous or high-tier issue goes through a reviewed `PRODUCT.md` + `TECH.md` spec PR; criteria, spec and holdout scenarios are then frozen and hashed. Holdout scenarios live in a private repo the builder cannot read and must fail on `main` before they count.
- **Independent gates:** judge, reviewer and scenario agents run on a different model family and a fresh context from the builder; findings must be verified before they block, and travel as a validated, line-anchored `review.json` posted by a separate job.
- **Blast radius:** no SSH keys for agents, GitHub Apps per role with least privilege, branch protection pinned to check sources, attested binaries, automatic rollback and a kill switch the agents cannot turn back on.
- **Cost:** runs on free-tier models and free public-repo Actions minutes; private minutes are budgeted and tracked.
- **Self-improvement with guardrails:** the factory may change its own prompts and router, but workflow files, graders, thresholds, branch protection and the kill switch are off-limits.

## Open questions

The spec tracks the unresolved ones: the target app's overarching requirements and roadmap, telemetry store, provider router and fallback, quota sharing with other pipelines, and spikes for the builder engine and orchestrator.

## Security

This repository is design documentation, but the design governs agents with write access, secrets and deploy rights. If you find a flaw in the design or in the repository configuration, report it privately — see [`SECURITY.md`](SECURITY.md). Please do not open a public issue for a security problem.
