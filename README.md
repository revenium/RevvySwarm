# RevvySwarm

[![Revenium Labs](https://img.shields.io/badge/Revenium-Labs-6f42c1?style=for-the-badge)](https://github.com/revenium/.github/blob/main/LABS.md)
[![Status: Beta](https://img.shields.io/badge/status-beta%20(best--effort)-f0a020?style=for-the-badge)](https://github.com/revenium/.github/blob/main/LABS.md)

> ### 🧪 This is a Revenium Labs project
> **Revenium Labs** projects are field-developed, best-effort solutions. They are working,
> beta-quality software, built to solve real customer problems and shared in the open. They are
> **not** part of Revenium's officially supported products.
>
> - It works and solves a real problem, but may need adaptation to fit your exact environment.
> - It's provided as-is, without the versioned-release guarantees, SLAs, or formal support
>   that back our core products.
> - We welcome your issues, feedback, and PRs, and **we're happy to work with you** to make it
>   fit your use case. [Come talk to us on Discord](https://discord.gg/J2DbmjZ2nA).
>
> → **[What is Revenium Labs?](https://github.com/revenium/.github/blob/main/LABS.md)**

<div align="center">
  <img src=".github/revvyswarm-icon.png" alt="RevvySwarm logo" width="140">

  **A terminal session manager for AI coding agents — with a native macOS app on top**

  <sub>Run Claude Code, Codex, Gemini CLI, and OpenCode sessions side by side, see which ones
  need you, and never lose one to a closed terminal tab.</sub>

  [![Licence](https://img.shields.io/badge/licence-proprietary%20(free%20to%20use)-blue?style=flat-square)](LICENSE.md)

  ### [Download Latest Release](https://github.com/revenium/RevvySwarm/releases/latest)

  <sub>macOS · Signed and notarized</sub>
</div>

---

## What is this?

If you run more than one AI coding session at a time, you know the problem: a pile of terminal
tabs, no idea which agent is waiting for input, and constant friction switching between
projects.

RevvySwarm gives you one place to see, switch, and manage every AI agent session — whether
you're running three or thirty. It's built on [tmux](https://github.com/tmux/tmux), so sessions
survive app restarts, crashes, and disconnects: SSH into the machine and your agents are still
running.

There are two ways to use it:

- **A native macOS desktop app** (the primary experience) — built with [Wails](https://wails.io/)
  (Go backend, React + [xterm.js](https://xtermjs.org/) frontend), with tabs, split panes, a
  command palette, and full searchable terminal scrollback.
- **A terminal UI (TUI)** — a [Bubble Tea](https://github.com/charmbracelet/bubbletea)-based
  interface for the same sessions, useful over SSH or if you just prefer to stay in the
  terminal. The desktop app and TUI share the same session data, so you can use either one, or
  both, interchangeably.

## Key features

- **Instant context switching** — tabbed interface with `Cmd+1–9` hotkeys in the desktop app.
- **Know what every agent is doing** — color-coded status (running / waiting / blocked / idle),
  activity ribbons showing how long a session has been waiting, and a flashing alert when an
  agent needs your attention.
- **Full terminal emulation** — xterm.js with searchable scrollback (`Cmd+F`), true color, and
  clickable links, backed by real tmux sessions so nothing is lost if the app closes.
- **Prompt navigation** — `Cmd+Up` / `Cmd+Down` jumps between every message you've sent an agent
  in the current session, skipping the tool calls and output in between.
- **Split panes** — work on multiple sessions side by side, save layout templates, zoom any pane
  full-screen.
- **Searchable session history** — every past Claude Code conversation is indexed and
  searchable by content, project, branch, and date, with AI-generated summaries so you can scan
  what a session was about at a glance. Resume any past session in one click.
- **Command palette (`Cmd+K`)** — switch sessions, launch a project, manage layouts, or run
  actions without touching the mouse.
- **Live context bar** — auto-detects GitHub PRs, Linear-style ticket IDs, dev server URLs, and
  git worktree paths from terminal output and surfaces them as clickable badges.
- **Git worktree support** — create a session in a new worktree/branch directly from the CLI.
- **Mobile access** — `revvy-swarm serve` hosts an installable web app so you can monitor and
  interact with sessions from your phone.

## Supported AI tools

| Tool | Status detection | Session resume | Fork | MCP management |
|------|-------------------|-----------------|------|-----------------|
| **Claude Code** | Running, waiting, blocked, idle, error | Yes (session ID) | Yes | Yes |
| **Gemini CLI** | Running, waiting, idle | Yes (session ID) | No | Yes |
| **OpenCode** | Running, waiting, idle | Yes (session ID) | No | No |
| **Codex / Cursor** | Basic prompt detection | No | No | No |
| **Shell / any CLI** | Prompt detection | N/A | N/A | N/A |

Claude Code has the deepest integration: automatic session ID capture, conversation forking, a
context-window meter, and auto-generated session notes.

## Requirements

- **macOS** for the desktop app (the underlying CLI and TUI also run on Linux and WSL, but this
  repository distributes the macOS app)
- **[tmux](https://github.com/tmux/tmux)** — `brew install tmux`
- At least one supported AI coding tool installed and signed in: [Claude
  Code](https://docs.anthropic.com/en/docs/claude-code), the `codex` CLI, [Gemini
  CLI](https://github.com/google-gemini/gemini-cli), or [OpenCode](https://github.com/opencode-ai/opencode)

## Install

1. **[Download the latest release](https://github.com/revenium/RevvySwarm/releases/latest)**
   — grab the `RevvySwarm-vX.Y.Z-darwin.zip` asset.
2. Expand it — double-click in Finder, or `ditto -x -k RevvySwarm-vX.Y.Z-darwin.zip .` from the
   command line. **Don't use `unzip`** — it can strip the code signature.
3. Drag `RevvySwarm.app` to `/Applications` and launch it. The app is signed with a Developer ID
   and notarized by Apple, so Gatekeeper opens it normally with no right-click workaround needed.
4. Install tmux if you haven't already: `brew install tmux`.

On first launch, RevvySwarm installs its CLI, sets up Claude Code integration (hooks for
auto-notes, a status line for the context meter), and walks you through adding your first
session.

Want to build it yourself instead? The application source lives in a private Revenium
repository — see [Contributing](CONTRIBUTING.md) for what's possible without access to it.

## Updates

New versions are published to this repository's [Releases
page](https://github.com/revenium/RevvySwarm/releases). To update, download the latest
release and repeat the install steps above — the new `.app` replaces the old one in
`/Applications`. RevvySwarm does not currently update itself automatically; check the Releases
page (or watch this repository) for new versions.

## Verifying a download

Every release is signed with a Revenium Developer ID and notarized by Apple. See
[SECURITY.md](SECURITY.md#verify-a-downloaded-release) for the exact commands to confirm a
download is authentic before you run it.

## Getting help

- **Bugs and feature requests:** [GitHub Issues](https://github.com/revenium/RevvySwarm/issues)
  on this repository — see [CONTRIBUTING.md](CONTRIBUTING.md) for what to include.
- **Questions, ideas, or just want to chat about it:** [Discord](https://discord.gg/J2DbmjZ2nA)
- **Security issues:** see [SECURITY.md](SECURITY.md) — please don't file these as public issues.

---

## Licence

RevvySwarm is **free to use, including commercially — but it is not open source.**
Revenium retains all rights to it, and the application source is not published.
You may install and use it on as many machines as you like; you may not
redistribute, mirror, or resell it. It comes with no warranty and no support
commitment, as Labs software does.

Full terms: [LICENSE.md](LICENSE.md). Open-source components bundled inside the
application remain under their own licences.

---

## Disclaimer

Not affiliated with, endorsed by, or sponsored by Anthropic PBC, OpenAI, or Google. Claude is a
trademark of Anthropic PBC; Codex and ChatGPT are trademarks of OpenAI; Gemini is a trademark of
Google. This is a session manager and terminal UI for tools you already use — it does not modify
or redistribute them.

<div align="center">
  <sub>Built by <a href="https://revenium.io">Revenium</a> · <a href="https://discord.gg/J2DbmjZ2nA">Discord</a></sub>
</div>
