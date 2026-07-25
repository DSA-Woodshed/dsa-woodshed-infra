# dsa-woodshed-infra Agent Guidance

This repository is the public DSA-Woodshed organization implementation
overlay skeleton, on the GF consumer pattern. **Status: SKELETON, gated on
TIN-2196 (GF consumer-registry v2), itself gated on TIN-3120.** Nothing here
is live. Do not add runner wiring, tofu stacks with real backends, or GF
consumer-registry entries ahead of that gate.

## Overlay, not ownership (TIN-1985 — verbatim doctrine)

Application repositories are **not** transferred into this org. This overlay
never owns or claims `Jesssullivan/dsa-study-packet` or
`Jesssullivan/dsa-woodshed.space`; they remain GF *consumers* under their
current owner. This overlay holds only the org tenant's own implementation
facts (App registration, runner enrollment config, apply-plane docs). Do not
propose repo transfers, do not add this overlay as a listed owner of either
app repo, and do not dual-list a consumer here and at the org tenant — GF
exchange precedence is spoke > consumer > org, and dual-listing is a
documented footgun.

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
- **Coordinate, don't reshape** the GF core consumer-registry. Registry
  schema and enrollment-eligibility rules are core-product-owned surface.
  This overlay proposes registry entries via PR when it is time; it does
  not unilaterally redefine registry shape or enum values.
- This repo is public: no employer names, no private estate substrate
  facts (cluster contexts, internal endpoints, bucket names), no personal
  logs. Only the publicly resolvable core product name (GloriousFlywheel)
  and generic GF-pattern conventions belong here until this tenant's own
  facts exist and are themselves cleared for a public repo.
