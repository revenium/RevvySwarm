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

  <sub>Run Claude Code and Codex CLI sessions side by side, see which ones need you,
  and never lose one to a closed terminal tab.</sub>

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
- **Know what every agent is doing** — color-coded status (running / waiting / blocked / idle)
  is driven by hooks Claude Code and Codex fire on real lifecycle events, so "done" means done,
  not just "the pane went quiet." Activity ribbons show how long a session has been waiting, and
  a flashing alert lets you know when an agent needs your attention.
- **Full terminal emulation** — xterm.js with searchable scrollback (`Cmd+F`), smooth continuous
  scrolling, true color, and clickable links, backed by real tmux sessions so nothing is lost if
  the app closes. Local and SSH sessions both get real native terminal scrollback.
- **Session Documents drawer (`Cmd+D`)** — every file a session created, edited, published,
  shared, or mentioned, gathered in one list per session, with quick actions to open it, reveal
  it in Finder, copy its path, hide it, or pin it. Works for remote (SSH) sessions too.
- **Prompt navigation** — `Cmd+Up` / `Cmd+Down` jumps between every message you've sent an agent
  in the current session, skipping the tool calls and output in between.
- **Split panes** — work on multiple sessions side by side, save layout templates, zoom any pane
  full-screen.
- **Searchable session history** — past Claude Code and Codex CLI conversations are indexed and
  searchable by content, project, branch, and date, with AI-generated summaries so you can scan
  what a session was about at a glance. Resume or fork a past session in one click.
- **Recovery and remote resilience** — resume stopped sessions one at a time or in bulk, and
  safely reconnect to or restart remote sessions.
- **Claude Code compatibility repair** — detects and guides repair for the fullscreen-TUI
  scrollback issue, so your terminal history remains usable.
- **Command palette (`Cmd+K`)** — switch sessions, launch a project, manage layouts, or run
  actions without touching the mouse.
- **Live context bar** — auto-detects GitHub PRs, Linear-style ticket IDs, dev server URLs, and
  git worktree paths from terminal output and surfaces them as clickable badges.
- **Git worktree support** — create a session in a new worktree/branch directly from the CLI.
- **Mobile access** — `revvy-swarm serve` hosts an installable web app so you can monitor and
  interact with sessions from your phone.
- **Decision Inbox (optional)** — agents can raise a structured question with options and a
  recommendation instead of blocking mid-conversation, and you answer it from one place — even
  pushed to your phone over Slack when you're away. See [What's new](#whats-new) below.

## What's new

In the latest release:

- **Real native terminal scrollback and smooth scrolling.** RevvySwarm now talks to tmux over
  its native control-mode wire protocol instead of screen-scraping a terminal, which means
  smoother, continuous scrolling and faster tab switching. It's on by default and works for both
  local and SSH sessions; if setup for a given tab fails for any reason, that tab automatically
  falls back to the older approach so you're never stuck. To turn it off everywhere, set
  `[features] control_mode_transport = false` in `~/.revvy-swarm/config.toml`.
- **Session Documents drawer (`Cmd+D`).** Every file a session touched — created, edited,
  published, shared, or just mentioned in conversation — now shows up in one list per session.
  Open it, reveal it in Finder, copy its path, hide it, or pin it. Press `Cmd+Shift+D` to expand
  it into a full tab. On by default.
- **Hook-driven status.** The colored status dot for each session (running / waiting / idle /
  done) is now driven by hooks Claude Code and Codex fire on real lifecycle events, plus explicit
  "done" and "paused" signals agents can send themselves — more accurate than just watching what
  the pane's text looks like. On by default.
- **Decision Inbox (off by default).** A "decision card" is a structured question an agent raises
  for you — a question, a couple of options, and a recommendation — instead of stopping and
  waiting mid-conversation. You answer it from the Inbox drawer or tab (`Cmd+Shift+I`) in the
  desktop app, from the mobile web app, or from the CLI, whenever it's convenient. Turn it on
  from Settings → Decisions (a restart is required).
- **Slack push notifications for the Decision Inbox.** With the Inbox on, an Away/Present toggle
  in the desktop app's top bar controls whether new cards also get pushed to your phone as a
  Slack DM with tap-to-answer buttons. Each person sets up their own Slack app through an
  in-app wizard in Settings → Decisions — nothing is shared between users. A
  `/revvyswarm alert|quiet|status` Slack command lets you flip Away/Present and check status
  from Slack itself.
- **Pane splits moved to `Cmd+\` and `Cmd+Shift+\`.** They previously lived on `Cmd+D` and
  `Cmd+Shift+D`, which now open the Documents drawer/tab instead.
- **First-run improvements.** RevvySwarm now explains up front why it's asking for Full Disk
  Access — it needs to read session data belonging to Claude Code and Codex, which macOS treats
  as another app's data — instead of just failing silently if you say no.

## Supported AI tools

| Tool | Status detection | Session resume | Fork | MCP management |
|------|-------------------|-----------------|------|-----------------|
| **Claude Code** | Running, waiting, blocked, idle, error | Yes (session ID) | Yes | Yes |
| **Codex CLI** | Tool-aware status and permission detection | Yes | Yes | Yes |
| **Gemini CLI*** | Running, waiting, idle | Yes (session ID) | No | Basic, where compatible |
| **OpenCode*** | Running, waiting, idle | Yes (session ID) | No | No |
| **Cursor / shell / any CLI** | Prompt detection | N/A | N/A | N/A |

Claude Code and Codex CLI are maintained, fully integrated experiences. Claude Code includes
automatic session ID capture, conversation forking, a context-window meter, and auto-generated
session notes. Codex CLI includes history search and summaries, native resume and fork, MCP
management, and restoration of captured model and effort settings.

\* Gemini CLI and OpenCode are best-effort compatibility integrations. They are not actively
maintained or regularly compatibility-tested.

## Keyboard shortcuts you'll use first

| Shortcut | Action |
|----------|--------|
| `Cmd+1–9` | Switch to tab N |
| `Cmd+T` | New tab |
| `Cmd+N` | New session |
| `Cmd+K` | Command palette |
| `Cmd+F` | Find in terminal |
| `Cmd+D` | Session Documents drawer |
| `Cmd+Shift+D` | Expand Session Documents to a tab |
| `Cmd+\` | Split pane right |
| `Cmd+Shift+\` | Split pane down |
| `Cmd+Up` / `Cmd+Down` | Jump between prompts |
| `Cmd+Shift+F` | Search past sessions |
| `Cmd+Shift+I` | Decision Inbox (once turned on in Settings) |

The full shortcut list is available in the app any time with `Cmd+/`.

## Requirements

- **macOS** for the desktop app (the underlying CLI and TUI also run on Linux and WSL, but this
  repository distributes the macOS app)
- **[tmux](https://github.com/tmux/tmux)** — `brew install tmux`. Use a reasonably recent
  version; the terminal transport RevvySwarm uses depends on tmux's control-mode protocol.
- At least one maintained AI coding tool installed and signed in: [Claude
  Code](https://docs.anthropic.com/en/docs/claude-code) or the `codex` CLI
- Optional, best-effort compatibility integrations: [Gemini
  CLI](https://github.com/google-gemini/gemini-cli) and [OpenCode](https://github.com/opencode-ai/opencode)

## Install

1. **[Download the latest release](https://github.com/revenium/RevvySwarm/releases/latest)**
   — grab the `RevvySwarm-darwin.zip` asset.
2. Expand it — double-click in Finder, or `ditto -x -k RevvySwarm-darwin.zip .` from the
   command line. **Don't use `unzip`** — it can strip the code signature.
3. Drag `RevvySwarm.app` to `/Applications` and launch it.
4. Install tmux if you haven't already: `brew install tmux`.

On first launch, RevvySwarm installs its CLI, sets up Claude Code and Codex integration (hooks
for auto-notes, session status, and a status line for the context meter), and walks you through
adding your first session. It will also ask for Full Disk Access — it needs this to read session
data that Claude Code and Codex store under macOS's protection as "another app's data"; you can
say no and use RevvySwarm without it, with reduced session discovery.

Want to build it yourself instead? The application source lives in a private Revenium
repository — see [Contributing](CONTRIBUTING.md) for what's possible without access to it.

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
application remain under their own licences — see
[THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md).

---

## Disclaimer

Not affiliated with, endorsed by, or sponsored by Anthropic PBC, OpenAI, or Google. Claude is a
trademark of Anthropic PBC; Codex and ChatGPT are trademarks of OpenAI; Gemini is a trademark of
Google. This is a session manager and terminal UI for tools you already use — it does not modify
or redistribute them.

<div align="center">
  <sub>Built by <a href="https://revenium.io">Revenium</a> · <a href="https://discord.gg/J2DbmjZ2nA">Discord</a></sub>
</div>
