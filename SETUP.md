# Setup Guide

This repo is the **book**. [Paperclip](https://github.com/paperclipai/paperclip) is the **software** the book teaches you to use. You read the book and you install Paperclip. This guide covers both and lists where the book's instructions have fallen behind Paperclip.

## The two repos at a glance

| | Headcount Zero (this repo) | Paperclip |
|---|---|---|
| **What it is** | A 14-chapter book in Markdown | A Node.js server and React dashboard for running AI agents as a company |
| **Author** | Anthony David Adams | Paperclip Labs |
| **License** | CC BY-NC-SA 4.0 (non-commercial) | MIT |
| **Pace of change** | Written March–April 2026 | Releases most days |
| **Setting it up means** | Reading it and keeping your fork in sync | Installing it and running it on your machine |
| **How they connect** | Chapter 5 explains Paperclip. Chapter 7 walks you through installing it. | The book is not mentioned in Paperclip |

## 1. The book

You can read it on GitHub. Start with the [table of contents](README.md#-table-of-contents).

To pull in future edits from the original author:

```bash
git remote add upstream https://github.com/AnthonyDavidAdams/zero-employee-company-book.git
git fetch upstream
git merge upstream/main
```

You can also use the **Sync fork** button on GitHub.

## 2. Paperclip

### Prerequisites

- **Node.js 24.11 or newer.** The book says 18. That is out of date. Check with `node --version`. With [nvm](https://github.com/nvm-sh/nvm), run `nvm install 24`.
- **A normal user account.** Do not use `sudo` or run as root, because the bundled Postgres database will not start as root.
- **An agent runtime with credentials,** so agents can do real work. One example is [Claude Code](https://code.claude.com/docs): install it, then run `claude` once to sign in. Instead of a subscription login, you can set `ANTHROPIC_API_KEY`. Signing in to Claude or Codex locally with a subscription also needs Python 3.

### Install and run

```bash
npx paperclipai@latest onboard --yes
```

This command:

- creates `~/.paperclip/instances/default` with the config, an embedded Postgres database, an encrypted secrets key and logs
- runs 12 health checks
- starts the dashboard at **http://localhost:3100**, reachable only from your own machine

Day-to-day commands:

| Task | Command |
|---|---|
| Stop | `Ctrl+C` |
| Start again later | `npx paperclipai run` |
| Check your setup | `npx paperclipai doctor` |
| Change settings | `npx paperclipai configure` |
| Get a permanent install with updates, rollback and a background service | `npx paperclipai install` |

Optional:

- **Use it from your phone or another computer.** Onboard with `--bind tailnet` (needs [Tailscale](https://tailscale.com)) or `--bind lan`. Both turn on login.
- **Turn off anonymous telemetry.** It is on by default. Set `PAPERCLIP_TELEMETRY_DISABLED=1` or `DO_NOT_TRACK=1`.
- **Take a throwaway test drive.** Run `ANTHROPIC_API_KEY=... npx paperclipai test-drive`. It starts a separate instance with a CEO agent already set up, and it uses your API key, which costs money.

### Your first company

Follow [Chapter 7](PART-3-HOW/07-open-your-terminal.md) from Step 2, with the changes in the next section. Paperclip's own [five-minute path](https://docs.paperclip.ing/guides/getting-started/five-minute-path/) covers the same ground for the current version.

## 3. Where the book is out of date

These were checked against `paperclipai` 2026.1005.0 in October 2026.

| Book says | Paperclip today |
|---|---|
| Node.js 18 or higher (Ch. 7) | **Node.js 24.11 or higher** |
| Dashboard at `http://localhost:3000` (Ch. 7) | **`http://localhost:3100`** |
| `npx paperclipai onboard --yes` (Ch. 0, 5, 7, 12) | Still works. Use `paperclipai@latest` so npx does not reuse an old cached copy. |
| "No API keys. No credit card." (Ch. 7) | True for installing Paperclip. Agents need a runtime that is signed in or has an API key before they can do any work. |
| "Bash script agent" runtime (Ch. 4, 7) | Now called the **Process** adapter. There are also built-in adapters for Claude Code, Codex, Gemini CLI, Cursor, OpenCode, OpenClaw, Hermes, Kimi, Pi and HTTP. |
| Work happens on heartbeat schedules. "Agent ignores a new task? Check the heartbeat." (Ch. 5, 7) | Agents now wake when they are assigned work or messaged. Timer heartbeats are optional. Recurring work uses **Routines**, triggered by cron, webhook or API. |
| "Sonnet-class gives the best balance" (Ch. 7) | Still good advice. Claude Code agents now **default to Opus**, so pick a Sonnet model yourself to keep costs down. |
| Cliphub marketplace "not live yet" (Ch. 5, 10) | There is still no public marketplace. **Ready-Made Teams** and company export/import now let you install and share pre-built teams. |

The budget warning at 80% and pause at 100% from Chapter 5 still match Paperclip's documentation.
