# Agent

This repository hosts a Hermes Agent — an autonomous AI coding agent built by
[Nous Research](https://hermes-agent.nousresearch.com) that drives a real web
browser and terminal to complete multi-step software tasks.

## What this Agent does

The agent in this repository is configured to operate via the CLI with the
default Hermes profile. It can:

- Inspect, search, and refactor codebases (multi-language, pygount-based).
- Author, run, and review code using delegated sub-agents (Claude Code, OpenAI
  Codex, OpenCode) for parallel, reasoning-heavy work.
- Drive a real browser over the Browser Use CLI for web automation:
  navigation, form filling (including vault-backed logins), data extraction,
  and scraping — with no screenshots required to reason (text-first).
- Take meeting/transcript notes, turn them into cited action items, and sync
  with calendars and task managers.
- Create and edit documents (Word, Excel, PowerPoint, Google Workspace, Notion,
  Obsidian) as well as PDFs (merge, fill, OCR, edit).
- Run system commands, debug Node.js / Python via the inspector, and exercise
  code through terminal sessions.
- Search the web, recover blocked/paywalled pages, and ground answers with
  cited, verifiable sources.
- Send and triage email, post to social platforms, and monitor competitors or
  product prices.
- Schedule local-only cron jobs (output saved to the cron log; not delivered
  back into a CLI session) and manage connections to hosted apps.

## Skills

Skills are loadable, reusable procedural packages under the default profile's
`skills/` directory. Each skill defines a trigger (first line) and the
step-by-step commands/workflow for a specific task type. Load a skill with
`skill_view(name='...')` before acting on that task, so you pick up the
author's preferred commands, pitfalls, and quality gates.

## Configuration

- Profile: `default` (lives under `~/.hermes/profiles/default/`).
- Each profile has its own independent `skills/`, `plugins/`, `cron/`, and
  `memories/` directories, so profile changes only affect that profile's
  sessions.
- The scratch/cache directory is `~/.hermes/cache/scratch` (`TMPDIR`), cleaned
  after 24 hours of idle.

## Running

Invoke a task and the agent will scan loaded skills for relevance, load any
matching skill, and execute the workflow. Background/delegated work that
delivers its result only after a turn ends is handed off explicitly — the agent
finishes non-dependent work first, then stops so delivery can occur.
