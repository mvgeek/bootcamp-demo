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
npm install
npm run dev
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

- [Claude Code](https://claude.ai/code) installed and authenticated
- Node.js 18+
- (Optional) [OpenAI Codex CLI](https://github.com/openai/codex) for independent code review
