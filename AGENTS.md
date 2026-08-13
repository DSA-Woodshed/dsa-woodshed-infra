# dsa-woodshed-infra Agent Guidance

This repository is the public DSA-Woodshed organization implementation
overlay skeleton, shaped for the GF consumer pattern. **Status:
NON-LOAD-BEARING SKELETON, gated on TIN-2196 (GF consumer-registry v2),
itself gated on TIN-3120.** The `2a033772` baseline is not empty, but nothing
here is live or authoritative infrastructure. Do not add runner wiring, tofu
stacks with real backends, or GF consumer-registry entries ahead of that
gate.

## Overlay, not product authority

The `DSA-Woodshed` organization is the planned future home of
`dsa-study-packet` and `dsa-woodshed.space`, after their separate durability
and cutover gates pass. The public decision and durability boundary live in
[dsa-woodshed-infra issue #4](https://github.com/DSA-Woodshed/dsa-woodshed-infra/issues/4).
That ownership move does not make this infrastructure repository an owner of
product code, content, rendering, or roadmap state. Issue #4 grants no transfer
permission by itself. Do not transfer either repository until every durability
box is complete and the repository administrator with transfer authority
explicitly approves that repository's action-time cutover after its settings,
integrations, rollback state, and exact head have been captured.

This overlay holds only the org tenant's future implementation facts: App
registration, runner enrollment config, and apply-plane docs. Do not describe
either product repository as a formally enrolled GF consumer until registry
and enrollment proof exists. Do not copy product code here or list a product
repository in both a per-repository GF consumer row and the organization-tenant
GF row proposed by this overlay. GF exchange precedence is spoke > consumer >
org, and dual-listing remains a documented footgun.

## Hard rules

- Do not commit secrets, `.env` files, kubeconfigs, private keys, PEMs, or
  backend credentials. There is no exception for "just a placeholder" —
  placeholders are empty strings or comments, never sample-shaped values.
- No GitHub App is created by an agent. `docs/github-app-manifest.md` is a
  reviewable **manifest document**, not an API call; App creation is an
  operator browser action.
- When an App is eventually provisioned for this tenant, it is **this
  tenant's own App** with **zero secret reuse** from any other overlay
  (GFTB, MMS, or any other owner). No shared PEM, no shared installation ID.
- Runner labels: only shared `tinyland-*` capability labels
  (`tinyland-nix`, etc.). Forbidden, without exception: repo-specific
  labels, project-identity labels, org-identity labels (e.g. `woodshed-*`,
  `dsa-woodshed-*`), and personal-account runner groups. A workflow
  requesting a forbidden label shape is treated as a bug, not a feature.
- Secrets never enter git. A `sops` lane is reserved for this overlay's own
  encrypted inputs when provisioning begins; it does not exist yet and this
  skeleton does not fabricate one.
- No workflow in `.github/workflows/` does anything but validate (lint /
  link-check). No plan/apply lane, no ARC deploy lane, exists until
  TIN-2196 clears.
- A site workflow being picked up by ARC on the shared `tinyland-docker`
  capability proves only `ARC_PICKUP`. It is not proof of GF
  consumer-registry enrollment, cache use, or RBE use for either application
  spoke.
- Use "remote-first maintainer validation," not "remote everything." Report
  `LOCAL_COMPAT`, `ARC_PICKUP`, `REMOTE_CACHE`, and `REMOTE_EXECUTION` as
  separate observed states. Never infer one from another. The minimum receipts
  are:
  - `LOCAL_COMPAT`: the named command passes without claiming a remote service;
  - `ARC_PICKUP`: the exact job records pickup by the intended ARC capability;
  - `REMOTE_CACHE`: a repeated build records an observed remote cache hit or
    transfer counter from the authorized cache; and
  - `REMOTE_EXECUTION`: an eligible named action records execution by the remote
    executor with local fallback excluded.
- **Coordinate, don't reshape** the GF core consumer-registry. Registry
  schema and enrollment-eligibility rules are core-product-owned surface.
  This overlay proposes registry entries via PR when it is time; it does
  not unilaterally redefine registry shape or enum values.
- This repo is public: no employer names, no private estate substrate
  facts (cluster contexts, internal endpoints, bucket names), no personal
  logs. Only the publicly resolvable core product name (GloriousFlywheel)
  and generic GF-pattern conventions belong here until this tenant's own
  facts exist and are themselves cleared for a public repo.
