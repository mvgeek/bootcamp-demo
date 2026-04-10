# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

This is the Mindvalley Bootcamp Demo — an AI-powered build pipeline that takes you from idea to working product using Claude Code skills.

## Branches

- **`main`** — The scaffolding. Clone this branch to start fresh. It contains only the AI skills (`/prd`, `/plan`, `/build`, `/codex-review`) in `.claude/skills/`, this file, and `.gitignore`. No project code. **Bootcamp participants should clone this branch.**
- **`demo`** — The complete reference project (an ASCII art generator) built using the pipeline. Switch to this branch to see the finished result, including source code, PRD, sprint plan, contracts, and reviews.

## Getting Started (Bootcamp Participants)

1. Clone the `main` branch:
   ```bash
   git clone <repo-url>
   cd bootcamp-demo
   ```
2. Open Claude Code in the project directory
3. Run `/prd new my-project-name` — describe your idea and Claude will help you write a PRD
4. Run `/plan` — Claude reads the PRD and generates a sprint plan
5. Run `/build` — Claude builds the entire project sprint by sprint, no intervention needed
6. When the build finishes, install and run:
   ```bash
   pnpm install
   pnpm build    # production build
   pnpm dev      # development server
   ```

## Skills

Skills live in `.claude/skills/` and are invoked as slash commands:

| Skill | What it does |
|-------|-------------|
| `/prd new <name>` | Create a new Product Requirements Document through guided conversation |
| `/plan` | Generate a sprint plan from the PRD |
| `/build` | Build the entire project automatically — sprint by sprint with evaluation |
| `/codex-review` | (Optional) Run an independent code review using OpenAI's Codex CLI |

## How the Build Pipeline Works

The `/build` skill runs a loop for each sprint:

1. **Generate** — A Claude agent implements the sprint
2. **Evaluate** — A separate Claude agent rigorously tests it
3. **Codex Review** — (Optional, requires Codex CLI) OpenAI reviews Claude's code for an independent second opinion
4. **Decide** — Pass moves to the next sprint; fail retries with feedback (up to 3 attempts)

Artifacts are written to:
- `prd/` — Product requirements
- `plans/` — Sprint plans
- `contracts/` — What each sprint built
- `reviews/` — Evaluation results

## YOLO Mode (Auto-Accept Permissions)

YOLO mode auto-approves all tool permissions so Claude can run the `/build` pipeline without interruptions. Ideal for walking away and letting it finish.

**To enable** (recommended for `/build`):
Create `.claude/settings.local.json` with:
```json
{
  "permissions": {
    "allow": [
      "Bash(*)", "Edit(*)", "Write(*)", "Read(*)",
      "Glob(*)", "Grep(*)", "WebFetch(*)", "WebSearch(*)",
      "NotebookEdit(*)", "ExitPlanMode(*)", "Agent(*)",
      "mcp__claude-in-chrome__*"
    ]
  }
}
```

**To disable** (require manual approval):
- Delete `.claude/settings.local.json` or replace its contents with `{}`

Note: `settings.local.json` is gitignored and stays local to each user's machine.

## Status Line

A global status line displays real-time session info at the bottom of Claude Code:

```
ctx [██████░░░░] 58%  ⏱ 12m  $1.24  main  S3/5·A1·GEN  T:34
```

Shows context window usage (color-coded), session duration, cost, git branch, build pipeline progress, and turn count.

During `/build`, the orchestrator writes `.claude/build-state.json` to communicate pipeline state (sprint, attempt, stage) to the status line. This file is gitignored and cleaned up after the build completes.

## Codex Review (Optional)

The build pipeline includes an optional independent review step using OpenAI's Codex CLI. If `codex` is not installed, the step is skipped automatically.

To install: `pnpm add -g @openai/codex` then `codex login` to authenticate.

To use standalone: `/codex-review` reviews all uncommitted changes.

## Prerequisites

See the [README](README.md) for detailed installation instructions for Git, Node.js, Claude Code, and (optionally) Codex CLI.

### Claude in Chrome Extension

The build and review skills can use browser automation to verify your running app. This requires the **Claude in Chrome** MCP extension:

1. Install the [Claude in Chrome](https://chromewebstore.google.com/detail/claude-in-chrome) extension from the Chrome Web Store
2. Enable it in Chrome and ensure it's running before starting a build
