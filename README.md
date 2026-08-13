# dsa-woodshed-infra

> **NON-LOAD-BEARING SKELETON** — gated on TIN-2196 (GF consumer-registry
> v2), itself gated on TIN-3120. The `2a033772` baseline is not empty: it
> contains documentation and placeholder configuration. Nothing in it is
> live infrastructure: no App, no runner, no apply plane.

## What this is

The org-tenant **implementation overlay** for The DSA Woodshed, on the same
GF consumer pattern as the estate's other owner overlays (Great-Falls-Tool-Bus
is the reference shape this repo mirrors at skeleton fidelity). When
provisioned, this repo will hold The DSA Woodshed's own GitHub App
registration facts, ARC/runner enrollment config, and apply-plane docs —
owner-specific facts, never reusable product logic.

## What this is not

- **Not a product authority.** The `DSA-Woodshed` organization is the planned
  future home of `dsa-study-packet` and `dsa-woodshed.space`, after each
  transfer gate passes. The public direction and durability boundary are
  recorded in [issue #4](https://github.com/DSA-Woodshed/dsa-woodshed-infra/issues/4).
  It grants no transfer permission: every durability box must be complete and
  the repository administrator with transfer authority must approve each
  action-time cutover separately.
  This overlay does not own their code, content, rendering, or roadmap state.
  **Overlay, not product authority** is the charter's spine.
- **Not a runner product.** Reusable ARC/controller modules, capability
  labels, and runner images are owned upstream by the GF core product, not
  by this overlay.
- **Not proof inferred from runner pickup.** A site workflow picked up by ARC
  on shared `tinyland-docker` proves only `ARC_PICKUP`. It does not prove GF
  consumer-registry enrollment, cache use, or RBE use for either application
  spoke.
- **Not "remote everything."** Future work is remote-first maintainer
  validation. `LOCAL_COMPAT`, `ARC_PICKUP`, `REMOTE_CACHE`, and
  `REMOTE_EXECUTION` are separate claims and must be reported separately using
  the minimum receipts defined in `AGENTS.md`.
- **No org-identity runner labels, ever.** Workflows in this org request
  shared `tinyland-*` capability labels only. A label like `woodshed-*` or
  `dsa-woodshed-*` is a forbidden shape regardless of provisioning state —
  see `AGENTS.md`.

## Current contract

No load-bearing infrastructure is populated. `config/organization.yaml`
carries the identity skeleton — known-today public facts plus explicit
placeholders for everything that depends on TIN-2196's exit. See:

- [`AGENTS.md`](AGENTS.md) — the boundary rules an agent must honor here.
- [`config/organization.yaml`](config/organization.yaml) — the identity
  skeleton.
- [`docs/onboarding-runbook.md`](docs/onboarding-runbook.md) — the gated
  enrollment ritual.
- [`docs/github-app-manifest.md`](docs/github-app-manifest.md) — the
  reviewable App manifest for when provisioning opens.
- [`docs/site-ruleset.md`](docs/site-ruleset.md) /
  [`docs/site-ruleset-draft.json`](docs/site-ruleset-draft.json) — a
  reviewable required-signatures draft for the site. It is not applied and is
  not a repository-transfer prerequisite.

## Boundary

This repo is public and company-neutral. It names only the publicly
resolvable core product (GloriousFlywheel) and public GF-pattern
conventions. It does not name private estate substrate (cluster contexts,
backends, internal cache endpoints) until those facts exist for this
tenant and are themselves safe to publish.
