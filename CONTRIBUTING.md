# Contributing to RevvySwarm

Thanks for using RevvySwarm and for considering contributing.

**A note on what this repository is:** this is the public download and distribution point for
RevvySwarm — it holds signed, notarized builds of the app, not the application source code. The
source lives in a private Revenium repository, so **pull requests aren't possible here.** That
doesn't mean there's nothing to contribute — bug reports, feature requests, and feedback from
real usage are genuinely useful and read by the people building the app.

## How to contribute

### Report a bug

Before filing one, check [existing issues](https://github.com/revenium/RevvySwarm/issues)
to avoid duplicates, and confirm you're on the latest release (Settings → About, or check the
[Releases page](https://github.com/revenium/RevvySwarm/releases)).

Open a [new issue](https://github.com/revenium/RevvySwarm/issues/new) and include:

- **App version** — Settings → About in the desktop app
- **macOS version** — Apple menu → About This Mac
- **Which AI coding tool you were using** — Claude Code, Codex, Gemini CLI, or OpenCode
- **What you expected vs. what happened**
- **Steps to reproduce**, if you can find a reliable one
- **Relevant logs**, if the bug is a crash or a session behaving unexpectedly:
  - App logs: `~/.revvy-swarm/logs/revvyswarm_*.log` (most recent file)
  - Desktop app frontend logs: `~/.revvy-swarm/logs/frontend-console.log`

Please don't include full log files with sensitive session content unless you've reviewed them
first — trim to the relevant lines where you can.

**Found a security vulnerability?** Don't open a public issue — see [SECURITY.md](SECURITY.md)
for how to report it privately.

### Request a feature or improvement

Open an [issue](https://github.com/revenium/RevvySwarm/issues) describing the problem
you're trying to solve, not just the feature you have in mind — the "why" helps us evaluate
whether it fits the tool and how urgently. Check existing issues first so we can consolidate
related requests.

### Ask a question or just talk to us

Open an issue, or come find us on [Discord](https://discord.gg/J2DbmjZ2nA). We're generally
responsive there and happy to talk through how you're using RevvySwarm or what's not working for
you.

## What to expect

RevvySwarm is a [Revenium Labs](https://github.com/revenium/.github/blob/main/LABS.md) project:
field-developed, best-effort software, not one of Revenium's officially supported products. That
means:

- No SLA on issue response time, though we do read and triage everything.
- Fixes and features ship at the maintainers' discretion, based on impact and effort.
- We're happy to work with you to make RevvySwarm fit your use case, but we can't commit to
  every request.

## Code of Conduct

Participation in this repository's Issues and any linked community spaces is governed by our
[Code of Conduct](CODE_OF_CONDUCT.md). Please read it before posting.

## Security

See [SECURITY.md](SECURITY.md) for supported versions, how to report vulnerabilities privately,
and how to verify that a downloaded release is authentic.
