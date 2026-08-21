# Security Policy

## Supported versions

Revenium provides security fixes for the latest release of RevvySwarm. Install the current
version from:

- [Revenium GitHub Releases](https://github.com/revenium/revvyswarm-releases/releases/latest)

## Report a vulnerability privately

Do not open a public issue for a suspected vulnerability.

Use this repository's
[private security advisory form](https://github.com/revenium/revvyswarm-releases/security/advisories/new).
If GitHub advisories are unavailable, email
[support@revenium.io](mailto:support@revenium.io) with:

- A description of the issue and its impact
- Reproduction steps or a proof of concept
- Affected versions and macOS versions
- Any suggested mitigation
- A safe way to contact you

Revenium will acknowledge the report, investigate it, coordinate remediation, and credit the
reporter when requested and appropriate.

## Sensitive data

RevvySwarm manages terminal sessions for AI coding agents and stores related metadata locally on
your Mac:

- Session metadata (titles, groups, working directories, status) is stored as JSON under
  `~/.revvy-swarm/`.
- Application logs are written to `~/.revvy-swarm/logs/`.
- Credentials for the AI tools themselves (Claude Code, Codex, Gemini CLI, OpenCode) are managed
  by those tools, not by RevvySwarm — it launches and monitors them, it does not read or store
  their API keys or session tokens.

Never include real API keys, OAuth tokens, session tokens, signing certificates, or diagnostic
archives containing personal data in a public issue.

## Release and update security

This repository does not contain RevvySwarm's source code — it exists to distribute signed,
built releases, because the source repository is private. Official releases published here are:

1. Built from a stable, tagged version of the private source repository
2. Signed with a Revenium-owned Developer ID Application identity
3. Submitted to Apple's notary service and stapled
4. Assessed by Gatekeeper
5. Packaged as a `.zip` archive containing the notarized `RevvySwarm.app` (GitHub publishes a
   SHA-256 digest for every release asset; no separate checksum sidecar is needed or published)
6. Distributed exclusively through this GitHub repository's Releases page

## Verify a downloaded release

Download `RevvySwarm-vX.Y.Z-darwin.zip` from the [release page](https://github.com/revenium/revvyswarm-releases/releases),
then:

1. Compare its checksum to the digest GitHub reports for that asset (shown on the release page,
   or via `gh release view <tag> --json assets`):

   ```bash
   shasum -a 256 RevvySwarm-vX.Y.Z-darwin.zip
   gh release view vX.Y.Z --repo revenium/revvyswarm-releases \
     --json assets --jq '.assets[] | select(.name == "RevvySwarm-vX.Y.Z-darwin.zip") | .digest'
   ```

   The two SHA-256 values must match.

2. Expand the archive with `ditto`, not `unzip` — `unzip` can strip the extended attributes that
   carry the code signature, causing verification to fail even on a genuine download:

   ```bash
   ditto -x -k RevvySwarm-vX.Y.Z-darwin.zip .
   ```

3. Verify the app's signature, notarization ticket, and Gatekeeper assessment before launching
   it:

   ```bash
   codesign --verify --deep --strict --verbose=2 RevvySwarm.app
   xcrun stapler validate RevvySwarm.app
   spctl --assess --type execute --verbose=4 RevvySwarm.app
   ```

   All three checks must pass before you trust and launch the app. A healthy result looks like:
   `valid on disk` / `satisfies its Designated Requirement` (codesign), `The validate action
   worked!` (stapler), and `accepted` with `source=Notarized Developer ID` (spctl).

For non-security bugs, use
[GitHub Issues](https://github.com/revenium/revvyswarm-releases/issues) on this repository.
