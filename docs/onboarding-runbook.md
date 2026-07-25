# DSA-Woodshed onboarding runbook (skeleton)

**GATED: TIN-2196** (GF consumer-registry v2), itself **GATED: TIN-3120**. No
step below is runnable today. This records the enrollment ritual's shape —
modeled on the Great-Falls-Tool-Bus overlay's onboarding runbook (org tenant
#3 on the same pattern) — so it does not need to be rediscovered when the
gates clear.

Prereqs (once gated work opens): an operator machine with `gh` authed as a
DSA-Woodshed org owner; the decided core repository and pin recorded in
`config/organization.yaml`; a decided state/cache backend for this tenant.

## 1. Create the org GitHub App (browser) — GATED: TIN-2196

Open `https://github.com/organizations/DSA-Woodshed/settings/apps/new`.

- Name: `gf-arc-dsa-woodshed` (per the `gf-arc-<owner-slug>` convention)
- Homepage URL: `https://github.com/DSA-Woodshed/dsa-woodshed-infra`
- Webhook: **UNCHECK Active**
- Permissions (ARC `github_config` requirements, exact and minimal — see
  [`docs/github-app-manifest.md`](github-app-manifest.md)): Organization ->
  Self-hosted runners: **Read and write**; Repository -> Actions:
  **Read-only**; Repository -> Metadata: **Read-only**
- Where can this App be installed: **Only on this account**
- Create; record the App ID from the app page.

## 2. Generate and download the private key (browser) — GATED: TIN-2196

App page -> Private keys -> Generate a private key. The `.pem` never enters
git: move it directly to operator-controlled local storage, record its
rotation path in the operator credential store, and go no further with it in
this repo than a filename reference.

## 3. Install the App on the org (browser) — GATED: TIN-2196

App page -> Install App -> DSA-Woodshed -> **All repositories** -> Install.
Capture the installation ID from the resulting URL or via
`gh api /orgs/DSA-Woodshed/installations`.

## 4. Populate this overlay's identity file — GATED: TIN-2196

Fill the `PLACEHOLDER` fields in `config/organization.yaml`: `core.*` (once
the tracked core repository and pin are decided), `owner.github_app_secret_name`,
and `substrate.*` (once this tenant's backend/cache facts are decided and
themselves cleared for a public repo — some may need to move to a private
downstream file instead of this public one).

## 5. Local validation — GATED: TIN-2196

Whatever the eventual `just`-front-door validation surface is for this
overlay, it runs read-only static checks (schema/taxonomy shape, `tofu fmt`
/ `validate` equivalents) with no cluster reachability required. Wire it
before step 6, not after.

## 6. Write the App credential into whatever backend this tenant lands on — GATED: TIN-2196

**Named, not scripted, here.** The concrete command depends on the backend
decided in step 4 and does not exist yet. Whatever it is: it consumes the
App ID, installation ID, and PEM path as inputs; it writes a named secret
(`github-app-secret-dsa-woodshed`, matching `config/organization.yaml`); and
it never prints or logs the PEM contents.

## 7. First plan (operator machine, bootstrap circularity) — GATED: TIN-2196

This overlay's own future CI would run on a `tinyland-*` label that, for an
org tenant, resolves only through this org's own scale set. Until the first
operator-machine apply succeeds, overlay CI queues unpicked — the same
bootstrap circularity GFTB records. The first plan and first apply happen
from an operator machine, never from this overlay's own CI.

## 8. Operator APPLY gate — GATED: TIN-2196

Plan review is a human step by design (creates-only, zero deletes expected
on a fresh state key). Apply is operator-gated; this skeleton does not
define an apply command because no backend exists yet to apply against.

## 9. Verify the listener — GATED: TIN-2196

Confirm the scale set registered and is Helm-managed, then re-run the local
validation surface from step 5 — it should now report the App-secret check
green and the scale set present.

## Step ledger

Every step above is `[operator-browser]` or `[operator-terminal]` except
step 4 (`[agent]`, editing this repo's tracked config) and step 5
(`[agent]`, running whatever read-only validation surface exists). No step
is `[agent]`-executed against a live App, secret store, or cluster; that
boundary does not move until an operator explicitly opens it, and even then
App creation, PEM handling, and apply consent stay human per
`docs/github-app-manifest.md` and `AGENTS.md`.
