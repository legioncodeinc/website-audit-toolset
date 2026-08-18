<!--
URL: https://github.com/krsnczky/agency-icm-builder
Fetch date: 2026-08-18
Source type: community post
Research cluster: audit-intake-workflow
Archived by: forge stage 2 sweep round 3 (deeper research pass, mcp__Exa__web_search_exa + mcp__Exa__web_fetch_exa), Website Auditor by Legion Code Inc., targeting previously-flagged thin coverage.
-->

# krsnczky/agency-icm-builder
URL: https://github.com/krsnczky/agency-icm-builder

Claude skill: build, audit, or restructure an AI-runnable workspace for a client-service agency. Folder structure does the orchestration.

- Stars: 3
- Forks: 0
- Watchers: 3
- Open issues: 0
- License: MIT License
- Default branch: main
- Created: 2026-07-23T16:20:05Z

## Top Contributors

- krsnczky (6 contributions)

---

## README

Agency ICM Builder

Build, audit, or restructure an AI-runnable workspace for a client-service agency.
Folder structure does the orchestration. Packaged as a Claude skill.

## Contents

- The idea
- What it does
- The shape it builds
- Install
- Layout
- Works well with
- Credits

## The idea

One agent, routing files, one folder per client, and a session-end capture protocol that turns daily work into durable memory. No framework, no database, no orchestration code. Markdown files in folders, arranged so that an agent always knows where it is, what to load, and where its work goes.

Extracted from a real system: these conventions run a marketing agency with 15 client folders and 5 service departments in daily production, built and hardened over months of real client work. This skill is the genericized version.

## What it does

Three modes:

- Build - interviews you about your agency (services, clients, the repeating unit of work, where humans check things), then scaffolds the full skeleton, ready before you grow into it rather than retrofitted under load. One client or fifteen, every kind of information gets a home from day one.
- Audit - checks an existing workspace against ten rules and reports findings with paths, costs, and smallest fixes. Read-only.
- Restructure - audit first, then a migration map for your approval, then migration. Your grown-wild folder usually already contains the structure informally; it gets extracted, not bulldozed.

## The shape it builds

```
agency/
├─ CLAUDE.md                # routes tasks to files; holds no content itself
├─ clients/
│  ├─ _template/            # new client = copy this
│  └─ acme-corp/
│     ├─ .claude/CLAUDE.md  # load order for this client
│     ├─ wiki/              # hot.md (now), log.md (history), profile, brand
│     ├─ memory/            # learnings.md (distilled rules)
│     └─ work/              # deliverables
├─ departments/             # stable expertise per service line
├─ workflows/               # multi-step sequences with human gates
└─ system/                  # load-order contract, capture rules, changelog
```

The core guarantees:

- Clients never mix. Everything about a client lives in its folder; uncertain attribution goes to a quarantine inbox instead of a guessed folder.
- Load per task, not per session. An explicit contract says which files each task type needs. The agent loads those and stops.
- Sessions end in capture. Log entry, state update, lesson learned, written back automatically, so week 30 of the workspace knows what week 1 learned.
- State is inspectable. Any human can open `hot.md` and `log.md` and see exactly where a client stands. No dashboard, no vendor.

## Install

Claude Code: copy this folder to `~/.claude/skills/agency-icm-builder/` (or `.claude/skills/agency-icm-builder/` inside a project), then say "build me an agency workspace", "audit my workspace", or "restructure this for agents".

Claude apps: zip this folder's contents and upload via Settings, then Capabilities.

## Layout

```
agency-icm-builder/
├─ SKILL.md                 the method: ten rules, three modes, the cold-read test
├─ references/
│  ├─ conventions.md        client triad, log tags, capture protocol, load-order contract
│  └─ enforcement.md        making conventions self-enforcing with Claude Code hooks
└─ assets/templates/        root CLAUDE.md, client template, department, workflow, interview
```

## Works well with

agency-memory-kit, a Claude Code plugin from the same production system that automates the memory side: session briefing hooks, context injection, and weekly memory consolidation. This skill builds the structure; the kit keeps it alive.

## Credits

The term ICM (Interpretable Context Methodology, folder structure as agent architecture) comes from Van Clief and McDermott, arXiv:2603.16021. The conventions in this skill were developed independently in production and share the methodology's core claim: for sequential, human-reviewed client work, the filesystem is the framework.

MIT licensed.
