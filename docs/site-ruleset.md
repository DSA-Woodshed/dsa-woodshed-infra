# Site required-signatures ruleset (drafted, not applied)

`docs/site-ruleset-draft.json` is a reviewable GitHub repository ruleset for
the site repository's default branch, modeled on the packet's active ruleset:
`Jesssullivan/dsa-study-packet` ruleset id `19697569`
(`main-required-signatures`, target `branch`, rule `required_signatures`,
enforcement `active`, no bypass actors). The draft strips the read-only
fields the GitHub API returns on GET (`id`, `node_id`, `source`,
`source_type`, `created_at`, `updated_at`, `_links`) that a POST body does
not accept, and re-points nothing else — this overlay does not invent a
different signing policy for the site than the one already proven on the
packet.

The site already has admin-enforced legacy branch protection with required
checks and force-push/deletion disabled. This draft adds signature enforcement;
it does not replace those checks or prove that transferred settings survived.

## Apply boundary

Do not infer a new signing-key requirement from an author email or a
checkout-local Git setting. Before applying this draft, verify the current
repository owner, inspect recent commits under every account that will merge,
and confirm that signature enforcement will not lock out maintainers. Apply it
only in a reviewed governance change after the destination protection state is
captured.

```bash
: "${TARGET_REPO:?set TARGET_REPO explicitly to OWNER/dsa-woodshed.space}"
case "$TARGET_REPO" in
  Jesssullivan/dsa-woodshed.space|DSA-Woodshed/dsa-woodshed.space) ;;
  *) echo "refusing unexpected target: $TARGET_REPO" >&2; exit 2 ;;
esac
ACTUAL_REPO="$(gh repo view "$TARGET_REPO" --json nameWithOwner --jq .nameWithOwner)"
test "$ACTUAL_REPO" = "$TARGET_REPO" || {
  echo "canonical repository mismatch: $ACTUAL_REPO" >&2
  exit 2
}
test "$(gh api "repos/${TARGET_REPO}/rulesets" \
  --jq '[.[] | select(.name == "main-required-signatures")] | length')" = 0 || {
  echo "main-required-signatures already exists; inspect it instead" >&2
  exit 2
}
gh api --method POST "repos/${TARGET_REPO}/rulesets" \
  --input docs/site-ruleset-draft.json
```

Run the block as a reviewed operator action with the target supplied explicitly;
do not paste only its final `gh api` line.
