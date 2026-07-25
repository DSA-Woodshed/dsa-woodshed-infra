# GitHub App manifest (review document, not a live manifest)

**GATED: TIN-2196.** This is a reviewable description of the App this
overlay would create, per the `docs/onboarding-runbook.md` ritual. It is a
**document**, not a POST-able manifest JSON and not a script — no agent
creates this App. GitHub's App-manifest flow (a browser form submission
that converts to App credentials on confirmation) is the intended operator
path; there is no full unattended-API creation path for a new App.

## Identity

| Field | Value |
|---|---|
| Name | `gf-arc-dsa-woodshed` (per the `gf-arc-<owner-slug>` convention) |
| Homepage URL | `https://github.com/DSA-Woodshed/dsa-woodshed-infra` |
| Owner | `DSA-Woodshed` organization |
| Webhook | **Off** (Active unchecked) |
| Install target | **Only on this account** (DSA-Woodshed), then **All repositories** at install time |

## Permissions

The minimum ARC `github_config` requires, and nothing wider:

| Scope | Access |
|---|---|
| Organization -> Self-hosted runners | Read and write |
| Repository -> Actions | Read-only |
| Repository -> Metadata | Read-only |

No other permission is requested. A future change that widens this table
needs its own review; do not add scopes speculatively.

## No-secret-reuse statement

This App, when created, is **this tenant's own App**. Its App ID,
installation ID, and private key are never shared with, copied from, or
copied to any other overlay (GFTB, MMS, or any other owner). No PEM is
committed to this repository or any repository. Rotation and custody live
in the operator's credential store, referenced by name only from tracked
docs (see `docs/onboarding-runbook.md` step 2).
