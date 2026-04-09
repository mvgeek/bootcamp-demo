# Mindvalley Bootcamp Demo

An AI-powered build pipeline that takes you from idea to working product using [Claude Code](https://claude.ai/code).

You describe your idea. Claude writes the PRD, plans the sprints, builds the code, and tests it — all automatically.

## Quick Start

```bash
git clone <repo-url>
cd bootcamp-demo
```

Then open Claude Code and run:

1. `/prd new my-project-name` — Describe your idea, Claude turns it into a structured PRD
2. `/plan` — Claude generates a sprint plan from the PRD
3. `/build` — Claude builds the entire project sprint by sprint (walk away, come back to a working app)

When the build finishes:

```bash
pnpm install
pnpm dev
```

## Branches

| Branch | Purpose |
|--------|---------|
| `main` | **Start here.** Clean scaffolding with just the AI commands. |
| `demo` | Completed reference project (ASCII art generator) built using the pipeline. |

## Commands

| Command | What it does |
|---------|-------------|
| `/prd new <name>` | Create a Product Requirements Document through guided conversation |
| `/plan` | Generate a sprint plan from the PRD |
| `/build` | Build the entire project automatically with evaluation loop |
| `/codex-review` | (Optional) Independent code review via OpenAI Codex CLI |

## Status Line

When you run `/build`, a status line at the bottom of Claude Code shows you live progress:

```
ctx [██████░░░░] 58%  ⏱ 12m  $1.24  main  S3/5·A1·GEN  T:34
```

This tells you at a glance: context window usage, session time, cost so far, which git branch you're on, and where the build pipeline is (Sprint 3 of 5, Attempt 1, currently Generating).

The status line is configured globally — it works in every project, not just this one. Outside of `/build`, the pipeline indicator disappears and you still see context, cost, branch, and turns.

## Optional: YOLO Mode

Auto-approve all Claude permissions so `/build` runs uninterrupted. Create `.claude/settings.local.json`:

```json
{
  "permissions": {
    "allow": [
      "Bash(*)", "Edit(*)", "Write(*)", "Read(*)",
      "Glob(*)", "Grep(*)", "WebFetch(*)", "WebSearch(*)", "Agent(*)"
    ]
  }
}
```

Delete the file to go back to manual approval.

## Prerequisites

You'll need the following tools installed before the bootcamp. Follow each step in order.

### 1. Git

Git is the version control tool used to clone this repo and track your changes.

- **Mac**: Open Terminal and run `xcode-select --install` (this installs Git along with other developer tools)
- **Windows**: Download and install from [git-scm.com](https://git-scm.com/download/win)
- **Linux**: `sudo apt install git` (Ubuntu/Debian) or `sudo dnf install git` (Fedora)

Verify it's installed:
```bash
git --version
```

### 2. Node.js (v18 or higher)

Node.js runs the JavaScript projects you'll be building.

- Download the **LTS** version from [nodejs.org](https://nodejs.org/)
- Or install via terminal:
  - **Mac** (with Homebrew): `brew install node`
  - **Windows**: Use the installer from the link above
  - **Linux**: `sudo apt install nodejs`

Verify it's installed:
```bash
node --version   # should show v18 or higher
pnpm --version
```

### 3. pnpm

pnpm is the package manager used by this project (a faster, more efficient alternative to npm).

**Install:**
```bash
npm install -g pnpm
```

Verify it's installed:
```bash
pnpm --version
```

### 4. Claude Code

Claude Code is the AI coding agent that powers the entire build pipeline.

**Install:**
```bash
pnpm add -g @anthropic-ai/claude-code
```

**Authenticate** (you'll need an Anthropic account or API key):
```bash
claude
```

This opens Claude Code and walks you through authentication on first run.

> If you don't have an Anthropic account, sign up at [console.anthropic.com](https://console.anthropic.com/)

Verify it's installed:
```bash
claude --version
```

### 5. (Optional) OpenAI Codex CLI

Codex CLI provides an independent code review from a different AI model (OpenAI) so Claude doesn't just review its own code. **This is optional** — the build pipeline works fine without it.

**Install:**
```bash
pnpm add -g @openai/codex
```

**Authenticate** (you'll need an OpenAI API key):
```bash
codex login
```

> Get an API key at [platform.openai.com/api-keys](https://platform.openai.com/api-keys)

Verify it's installed:
```bash
codex --version
```

### Checklist

Run this to verify everything at once:
```bash
git --version && node --version && pnpm --version && claude --version && codex --version 2>/dev/null || echo "Codex not installed (optional)"
```

You should see version numbers for at least Git, Node, and Claude Code.
