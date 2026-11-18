# Product management context engineering

This repository is your product management knowledge base and agentic workspace. You use it to connect durable product context to day-to-day PM work (strategy, discovery, delivery, alignment) so assistants behave like teammates who read your docs.

The [`.productmap/`](.productmap/) folder follows the same taxonomy you get from [Product Map](https://www.productmap.io/) when you sync or mirror the platform. On top of that tree, [AGENTS.md](AGENTS.md), [CLAUDE.md](CLAUDE.md), and [GEMINI.md](GEMINI.md) spell out how agents should behave; repeatable workflows live under [`.claude/skills/`](.claude/skills/) (Claude Code) and [`.gemini/skills/`](.gemini/skills/) (Gemini-oriented). You can point Claude, Codex, Gemini, and Cursor at one versioned source of truth instead of restarting context in every tool.

> **[Product Map](https://www.productmap.io/) is the AI operating system for product decisions.** Product context in. PM decisions out. Your coding agents build them.
>
> [Website](https://www.productmap.io/) · [Web app](https://app.productmap.io/) · [Install the plugin for Cursor, VS Code, and Antigravity](https://www.productmap.io/product-management-agents-for-cursor-vscode)

## Get started with this repository

**What you are building.** Product Map AI and the `.productmap/` tree are your context engineering and knowledge layer: curated lifecycle topics, templates, and frameworks in files agents can read. Cursor, Claude Code, Codex, and Gemini CLI sit on top as different runners; you pick the tool for the job and keep one repo as the handoff surface.

**A setup that works well**

- **Cursor** as the hub. Open this repo as the workspace so chat and edits see [AGENTS.md](AGENTS.md), [CLAUDE.md](CLAUDE.md), and [GEMINI.md](GEMINI.md) without path gymnastics. Use the Claude Code plugin for workflows that match [`.claude/skills/`](.claude/skills/). Use the Codex plugin with the same repo so Codex follows [AGENTS.md](AGENTS.md) (mirrored in [`.codex/README.md`](.codex/README.md)) and [`.codex/skills/`](.codex/skills/) (see [`.codex/skills/README.md`](.codex/skills/README.md)).
- **Claude Code** for skill-driven PM runs. The plugin reads [CLAUDE.md](CLAUDE.md) and routes recurring jobs through the right skill under [`.claude/skills/`](.claude/skills/) instead of one-off prompts.
- **Codex (inside Cursor)** when you want Codex-specific behavior and repo-local skills. Keep initiative outputs under `.productmap/00_company/product/` and raw inputs under `.productmap/10_data/` as [AGENTS.md](AGENTS.md) describes.
- **Gemini CLI** for jobs that need long-context synthesis, structured multi-section docs, or batch turns over the same tree. Install the Gemini CLI, open terminal in Cursor, `cd` to this repo, and rely on [GEMINI.md](GEMINI.md) plus [`.gemini/skills/`](.gemini/skills/) (see [`.gemini/README.md`](.gemini/README.md)). Optional: [`.gemini/settings.json`](.gemini/settings.json) for CLI defaults.
- **Product Map plugin** ([install](https://www.productmap.io/product-management-agents-for-cursor-vscode)) to run PM agents inside Cursor, VS Code, and Antigravity on this repo, next to Claude Code, Codex, and Gemini CLI. Agents read your product context before every run and propose edits as diffs you accept or discard.
- **Product Map AI** ([app](https://app.productmap.io/)) to run the same [agents](https://app.productmap.io/agents) and [workflows](https://app.productmap.io/workflows) in the browser, on the map you mirror into `.productmap/`. Sync or copy from the platform when you want the repo to stay the single file-based source of truth.

**Steps**

1. Clone or copy this repository and open it in Cursor.
2. In [Product Map AI](https://app.productmap.io/) or on the platform, sync or export so `.productmap/` matches the taxonomy and content you care about. Treat manual edits under `.productmap/` as intentional; otherwise you risk drift from the platform.
3. Skim [`.productmap/INDEX.md`](.productmap/INDEX.md) (or `.productmap/index.md`) so you know where templates, frameworks, and overviews live.
4. For day-to-day PM work in Cursor, `@`-mention or paste paths to the relevant `_overview.md` files and `09_templates/` files instead of pasting unstructured blobs into chat.
5. For a recurring task (PRD, roadmap narrative, KPI spec, research synthesis), open the matching folder under [`.claude/skills/`](.claude/skills/) or [`.gemini/skills/`](.gemini/skills/) and follow `SKILL.md` rather than improvising.
6. For Codex in Cursor, match the task to a skill under [`.codex/skills/`](.codex/skills/) when one exists; ground answers in `.productmap/index.md` first.
7. Put initiative-specific artifacts in `.productmap/00_company/product/`. Put interviews, exports, and raw feedback in `.productmap/10_data/`.
8. Use absolute dates (`YYYY-MM-DD`) in anything you write back to the repo.

You stay the orchestrator: same knowledge layer, different agents for different strengths; the repo is where outputs compound.

## What context engineering means for you

**Context engineering** means you choose what an agent sees, in what format, and in what order, so outputs stay consistent, reviewable, and tied to the product. You shape the whole environment around the task, not only the line you type into the chat box.

PM-oriented context engineering covers more than prompt engineering (one question, one reply) and more than context stuffing (pasting every PDF into the window). In practice it does three jobs:

- Separates roles: instructions (how the agent should act), durable knowledge (facts, templates, decisions), retrieval (large or fast-changing sources), and runtime context (the live initiative, ticket, or interview batch).
- Slows drift: when priorities, messaging, and constraints move every week, shared files beat everyone keeping a private story in chat threads.
- Stays repo-first: Git gives history, review, rollback, and portability. Your team owns the text in files you can branch and diff.

Think in four layers: canonical project knowledge, then agent instruction files, then runtime task context, then personal preferences. Keep root instruction files short. Link to [`.productmap/INDEX.md`](.productmap/INDEX.md) and templates; pull deeper files only when the task needs them.

## TASK: topics, agents, skills, knowledge

The [TASK framework](https://www.productmap.io/task-agentic-product-management) (Product Map, 2026-04-02) names how agentic PM work fits together. You stay the orchestrator. Scoped helpers run in clear domains on your product context; you keep judgment and calls.

| Pillar | Role |
|--------|------|
| T: Topics | PM domains and expert-led resources; the space where work happens (strategy, generation, analysis, delivery, people). |
| A: Agents | Scoped executors (research, drafting, prioritization, synthesis) with prompts, memory, and access to the right files. |
| S: Skills | Your competences and quality bars: what to delegate, how to steer agents, where to step in. |
| K: Knowledge | Outputs that compound: specs, roadmaps, research, decision logs; plain text, versioned, written back each cycle. |

### A loop you can run

- Start with one PM domain you are in today (discovery, analytics, delivery, and so on).
- Define or refine an agent: system prompt, tools, and which folders it may read or write.
- Apply your skills: steer output, set the bar, validate.
- Write back to the repo under `.productmap/` and raw inputs under `10_data/` so the next task reuses work.

Each pass gets faster when knowledge compounds and context stays clean. When output is wrong, thin, or stale, you fix the source: the instruction or file that led to it.

## Agent skills ([skills.sh](https://skills.sh/) ecosystem)

This repository is structured so the open [`skills`](https://github.com/vercel-labs/skills) CLI can discover installable skills: each skill is a folder with a `SKILL.md` that includes YAML frontmatter (`name` and `description` as plain strings). Skills live under [`.claude/skills/`](.claude/skills/) (Claude Code), [`.codex/skills/`](.codex/skills/) (Codex), and [`.gemini/skills/`](.gemini/skills/) (Gemini CLI). The CLI scans `.claude/skills/` and `.codex/skills/` on its own. [`skills.sh.json`](skills.sh.json) adds `.gemini/skills/` to its search paths, so the Gemini skills install from their real files (`SKILL.md` plus `subagent-prompt.md`).

Every `SKILL.md` ends with a "Related on Product Map" section that links the matching [agents](https://app.productmap.io/agents) and [workflows](https://app.productmap.io/workflows), so you can run the same job on your own product context.

A healthy clone should report **31** discoverable skills (11 Claude + 10 Codex + 10 Gemini). After you publish the repo to **public GitHub**, others can install with `npx skills add owner/repo`; [skills.sh](https://skills.sh/) lists the broader registry and ranks by anonymous install telemetry—full-text search there can lag behind a working local `npx skills add . --list`.

```bash
# List skills the CLI discovers from this repo (run from a clone)
npx skills add . --list

# After publishing: install from your public fork into an agent
npx skills add YOUR_GITHUB_USERNAME/product-management-context
```

## How this repository supports that workflow

- [`.productmap/`](.productmap/). Topics, frameworks, and templates along the product lifecycle.
- [`AGENTS.md`](AGENTS.md) and [`CLAUDE.md`](CLAUDE.md). Entry points that send agents to the index and house rules.
- Skills. Repeatable PM jobs with steps and guardrails: [`.claude/skills/`](.claude/skills/) for Claude Code, [`.gemini/skills/`](.gemini/skills/) for Gemini CLI (see [`.gemini/README.md`](.gemini/README.md)).
- Codex skills. Repo-local PM skills for Codex: [`.codex/skills/`](.codex/skills/) (see [`.codex/skills/README.md`](.codex/skills/README.md)).
- [`skills.sh.json`](skills.sh.json). Tells the `skills` CLI to also look for skills under `.gemini/skills/`.

If you edit `.productmap/` by hand, treat it as drift from the platform unless you mean to own that change.

## Product Map: the AI operating system for product decisions

AI-native teams ship fast. Engineering and design already have AI agents. Product does not. The bottleneck has moved from shipping to deciding what to build, for whom, and why.

[Product Map](https://www.productmap.io/) is the agentic product management operating system for AI-native product teams. Connect your product context once. PM agents then handle strategy, specs, pricing, and go-to-market, grounded in your product and proven PM practice. Decisions go straight to your coding agents to build.

Three pillars hold it together:

- **Multi-user, multi-agent.** People and agents share one environment, organized on top of your product context. Everybody works from the same picture instead of isolated chats.
- **Agentic workflows.** Agents perform PM tasks chained in workflows, all grounded in your product context instead of generic prompts.
- **Knowledge-backed.** Every decision draws on industry-standard frameworks and resources from top PMs, right when you make it.

Where you can run it:

- **In your IDE.** The [Product Map plugin](https://www.productmap.io/product-management-agents-for-cursor-vscode) runs PM agents in Cursor, VS Code, and Antigravity, next to your coding agents.
- **In the browser.** The [web app](https://app.productmap.io/) has the full catalog of [AI agents](https://app.productmap.io/agents) and [AI workflows](https://app.productmap.io/workflows) that take your product from strategy through delivery to go-to-market.
- **In this repo.** The `.productmap/` tree and the skills here are the open, file-based version of the same context layer.

## Install Product Map in Cursor, VS Code, or Antigravity

**[Install the plugin](https://www.productmap.io/product-management-agents-for-cursor-vscode)** and turn your IDE into a PM workspace that knows your product.

1. Install Product Map for Cursor, VS Code, or Antigravity from the [plugin page](https://www.productmap.io/product-management-agents-for-cursor-vscode), and open it in the workspace that holds your product context repo. A clone of this repository works.
2. Sign in with your Product Map account to set up the project knowledge base and connect it to Git.
3. Pick the agents you need, review their output, and push the updated artifacts to your repository.

The plugin is free, and a free account connects your project. It works in Cursor, VS Code 1.100 or later, and Antigravity, alongside Claude Code, Codex, Gemini CLI, and GitHub Copilot. Agents propose changes as diffs, and nothing is committed until you accept.

More AI PM agents from Product Map: https://www.productmap.io/
