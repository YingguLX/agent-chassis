# Agent Chassis

> **Not a prompt. A constraint skeleton.** 🏗️

Agent Chassis is a context and constraint engineering template for AI-assisted development. It replaces the chaotic "single giant system prompt" approach with six controlled project documents: each document has isolated responsibility, synchronized versioning, clear conflict priority, public fact boundaries, and an automatic quality guard that runs inside ordinary work.

This repository root `README.md` is the public GitHub homepage for Agent Chassis. The `README.md` created inside an instantiated target project is different: it is one of the six controlled documents and participates in that project's six-document synchronization.

---

## Why You Need This 🤔

Modern AI coding tools often rely on one oversized instruction blob. That creates predictable failure modes:

- **🗑️ Bloated & Chaotic** — Engineering rules, project facts, to-do plans, and user docs get mixed together.
- **📉 Weakened Over Time** — Strong constraints quietly degrade from "must" to "should" during maintenance.
- **🌊 Context Drift** — Agents read and write without clear ownership, and completed work disappears after context refresh.
- **🎯 Misapplied Templates** — Rules for one stack get treated as universal facts for every project.

Agent Chassis is **constraint engineering**. 🛡️ It does not teach agents how to sound helpful; it gives them a maintained skeleton for project entry, agent rules, engineering rules, factual baseline, evidence-backed to-do plan, user-facing docs, and quality control.

---

## How to Use It 🧭

Use Agent Chassis in two steps:

1. Copy the six controlled document templates under `agent-chassis/` into your target project root.
2. Copy the text from `BOOTSTRAP.md` into your AI agent chat to instantiate those templates against the target project's real facts.

`BOOTSTRAP.md` is a one-time bootstrap prompt. Copy its text into the chat; do not copy the file into the target project. It is not a seventh controlled document, not a runtime rule, not part of version synchronization, and not part of later project maintenance. After instantiation, ongoing work is governed by the target project's own `README.md`, `AGENTS.md`, `agents/RULES.md`, `agents/BASE.md`, `agents/TODO.md`, and `doc/DOCUMENTATION.md`.

---

## The Six-Document Skeleton 🦴

```text
project-root/
├── README.md              <- Human entry: what this is and where to start
├── AGENTS.md              <- Agent entry: loading rules, priority, quality guard
├── agents/
│   ├── RULES.md           <- Engineering rules and detailed quality guard
│   ├── BASE.md            <- Current factual baseline
│   └── TODO.md            <- To-do plan and confirmed known issues
└── doc/
    └── DOCUMENTATION.md   <- Formal user manual
```

The six documents are not interchangeable. `README.md` is the project-facing entry, `AGENTS.md` is the agent execution entry, `agents/RULES.md` is the detailed rulebook, `agents/BASE.md` records current facts, `agents/TODO.md` records evidence-backed follow-up work, and `doc/DOCUMENTATION.md` is the public user manual.

This root homepage is outside that skeleton. It explains the template as a public open-source project; it is not copied as the instantiated project's controlled `README.md`.

---

## Features & Innovations ✨

### Automatic Quality Guard

Quality control is embedded into ordinary work. Users do not manually operate checklists, command stages, or phase selectors. The agent selects lightweight or full coverage from task risk and impact scope, then reports the quality result as part of the normal task outcome.

The lightweight chain covers the `incremental difference domain`, `incremental security domain`, `factual boundary domain`, and `document quality domain`. The full chain covers the `public impact domain`, `global security domain`, `structural coverage domain`, and `manual output domain`. When a later domain is needed, earlier domains in the same chain are implicitly covered too.

### Public Entries, API, and ABI

Agent Chassis treats a public entry as any user-visible, user-obtainable, and user-verifiable API, CLI, SDK, service, plugin, protocol, configuration, UI, data format, model entry, deployment entry, operations entry, or documentation entry. API and ABI are kept separate: API is a user-facing usage contract; ABI exists only when binary compatibility commitments exist. Projects without binary commitments should not invent ABI facts.

### Factual Baseline

`agents/BASE.md` records current facts only. Missing evidence becomes `not applicable`, `not established`, or `pending confirmation`; it does not become a fabricated capability.

### Evidence-Backed To-Do Plan

`agents/TODO.md` records confirmed follow-up work, known issues, evidence locations, first actions, and verification suggestions. It is not a bucket for guesses, vague future ideas, or template placeholders.

### Formal User Manual Boundary

`doc/DOCUMENTATION.md` is based on public facts. It explains released or explicitly marked preview capabilities, and it must not expose internal maintenance flows or redefine project facts.

---

## Quick Start ⚡

```bash
# 1. Copy the six controlled document templates into your project root
#    from the agent-chassis/ directory in this repository.

# 2. Open BOOTSTRAP.md and paste its text into your AI agent chat.

# 3. Review the parameter confirmation report.
#    Confirm project_root, template_root, output_map, version, date,
#    fact sources, import policy, and text format policy.

# 4. Confirm execution only after the parameters are correct.

# 5. After instantiation, point your agent at AGENTS.md.
codex --instructions AGENTS.md
```

---

## Design Principles 🏗️

- **Constraints over suggestions.** "Must" stays "must." 🔒
- **Isolation over mixing.** Six documents, six jobs. 📦
- **Automatic quality over manual ceremony.** The guard runs inside ordinary work. ⛓️
- **Placeholders over fabrication.** `{{%...%}}` means "fill from evidence," not "make something up." 🎯
- **Public facts over private assumptions.** User-visible entries, API/ABI boundaries, and manual content must trace to evidence. 🧭

---

*Built for people who are tired of context drift.* 🏹
