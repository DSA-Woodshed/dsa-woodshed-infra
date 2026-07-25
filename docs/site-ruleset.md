# Site required-signatures ruleset (drafted, not applied)

`docs/site-ruleset-draft.json` is a ready-to-POST GitHub repository ruleset
for `Jesssullivan/dsa-woodshed.space`'s default branch, modeled exactly on
the packet's own active ruleset:
`Jesssullivan/dsa-study-packet` ruleset id `19697569`
(`main-required-signatures`, target `branch`, rule `required_signatures`,
enforcement `active`, no bypass actors). The draft strips the read-only
fields the GitHub API returns on GET (`id`, `node_id`, `source`,
`source_type`, `created_at`, `updated_at`, `_links`) that a POST body does
not accept, and re-points nothing else — this overlay does not invent a
different signing policy for the site than the one already proven on the
packet.

## The one blocker

The operator signing identity `jess@xoxd.ai` is **unverified** on the
account that would create this ruleset. `required_signatures` enforcement
would fail closed for that identity's own commits until it verifies. This
is the single thing gating apply; nothing else about the draft is
provisional.

## Apply, once cleared

```bash
gh api --method POST repos/Jesssullivan/dsa-woodshed.space/rulesets --input docs/site-ruleset-draft.json
```
