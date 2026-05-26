# README

> **Not a prompt. A constraint skeleton.** 🏗️

Agent Chassis is a context engineering template for AI-assisted development. It replaces the chaotic "single giant system prompt" approach with six controlled documents — each with isolated responsibilities, version-locked integrity, clear priority arbitration for conflicts, hard execution gates, and self-protecting rules.

---

## Why You Need This 🤔

Today's AI coding tools (CodexCLI, Claude Code, Cursor, etc.) all rely on one massive system prompt to constrain agent behavior. The problems are obvious:

- **🗑️ Bloated & Chaotic** — Engineering rules, project facts, todos, and user docs all crammed together. Nobody can make sense of it.
- **📉 Weakened Over Time** — To save tokens, "must" slowly becomes "should." Constraints get diluted with no one watching.
- **🌊 Context Drift** — Subagents read and write freely. Context drifts. Completed tasks vanish without a trace.
- **🎯 Misapplied Templates** — Templates written as absolute truth. C++ ABI rules forced onto Python projects.

Agent Chassis isn't prompt engineering. It's **constraint engineering**. 🛡️ It doesn't teach models how to sound human — it defines hard boundaries that machines can enforce.

---

## How to Use Them 🧭

Use Agent Chassis in two separate steps: first place the six controlled document templates in your target project, then instantiate those templates for that project's real facts.

For agent-assisted setup, open `BOOTSTRAP.md` in this repository and copy its prompt text into your AI Agent chat after the six templates are in the target project. The bootstrap prompt tells the agent to confirm paths, fact sources, output boundaries, version data, and quality checks before it writes the project-specific controlled documents.

`BOOTSTRAP.md` is not a seventh controlled document. Do not copy it into the target project, do not version-sync it with the six documents, and do not treat it as the runtime rulebook. After instantiation, ongoing AI-assisted development runs through the project's own `README.md`, `AGENTS.md`, `agents/RULES.md`, `agents/BASE.md`, `agents/TODO.md`, and `doc/DOCUMENTATION.md`.

---

## The Six-Document Skeleton 🦴

```text
project-root/
├── README.md              ← Human entry: What is this, where to start
├── AGENTS.md              ← Agent manual: How to execute, orchestrate, who decides
├── agents/
│   ├── RULES.md           ← Engineering red lines: What you can use, what you can't touch
│   ├── BASE.md            ← Fact baseline: Current state, what exists, where it is
│   └── TODO.md            ← Task ledger: What was done, what's left, where's the evidence
└── doc/
    └── DOCUMENTATION.md   ← User manual: How end users use this product
```

These six documents aren't randomly split. Their responsibilities, read/write permissions, modification thresholds, and conflict resolution order are all built in. 🔧

---

## Features & Innovations of Each Document ✨

### 1. README.md — Human-First Entry, Not a Machine Dump 👤

**Traditional approach:** The first file in the system prompt. Humans and machines read it together. It grows longer and longer.

**Agent Chassis approach:**

README.md speaks only to humans. It answers three questions: What is this, who should use it, where to start. It carries no agent execution rules, engineering red lines, or task tracking. After reading README, machines **must** navigate to AGENTS.md — never treat README as a universal context dump.

**💡 Innovation:** For the first time, "human entry" and "machine entry" are separated. README doesn't need to be memorized by the model. It just needs to tell humans how to find AGENTS.md.

---

### 2. AGENTS.md — The Agent Constitution, Not a Suggestion List 📜

**Traditional approach:** Scattered behavioral prompts: "Please ensure...", "It is recommended...", "It would be best if..."

**Agent Chassis approach:**

AGENTS.md is the agent's rulebook, speaking in **must / must not / can only**. It defines:

- **🔒 Trigger-Command Prefix Chains** — `Run Diff Review` → `Run Security Awareness` → `Run Factual Boundary Check` → `Run Documentation Proofread` (lightweight group). Full group: `Run Impact Assessment` → `Run Security Scan` → `Run Static Analysis` → `Run Documentation Generation`. The next stage **must not** start until the previous one completes. This isn't a suggestion — it's a hard gate.
- **👁️ Subagent Type Binding** — `explore` is read-only; `general` can write. Different subagents for reading and writing, preventing the "let me just fix this while I'm here" overreach.
- **🧾 Read Receipt** — Every time an agent reads AGENTS.md, its next visible response must declare the current version and briefly summarize the file. Prevents "pretending to have read it."
- **⚡ Load Check** — When the user message contains the exact literal `test build rules`, the agent must reply directly with the version number and summary. No tools. No misinterpreting it as a build/test request.

**💡 Innovation:** Turns "polite requests in a prompt" into "machine-verifiable execution protocols." Trigger commands are switches, not suggestions.

---

### 3. agents/RULES.md — Engineering Red Lines That Self-Protect 🛡️

**Traditional approach:** Coding standards written in some corner. Nobody checks them. Agents don't take them seriously.

**Agent Chassis approach:**

RULES.md is a shared engineering constraint for developers **and** agents — not a private agent prompt. It specifies language versions, dependency management, code style, test coverage, module boundaries, security rules, performance ceilings.

But the killer feature is **Chapter 13: Anti-Weakening Gate**:

> "Rules must not be weakened to make agent work easier. If a rule is too strict, **modify the rule explicitly** — do not ignore it."

This means:

- You can't change "must run markdownlint" to "recommended to run"
- You can't change "all six documents must sync versions" to "try to keep them in sync"
- You can't change "next stage must not start if previous failed" to "depends on the situation"

**💡 Innovation:** The constraint system comes with its own immune system. It knows someone (or some agent turn) will weaken "must" to "should" to save effort — so it blocks that path in advance.

---

### 4. agents/BASE.md — Fact Baseline, Not a Wishlist 📊

**Traditional approach:** Templates filled with "planned" features. Agents treat unimplemented capabilities as delivered promises.

**Agent Chassis approach:**

BASE.md records only the **current true state**: directory responsibilities, implemented public entries, build status, test entries, known issues, recent changes. Unimplemented capabilities **must** be marked `not established` or `not applicable` — never fabricated.

**Key distinction:**

- API = user-visible usage contract
- ABI = binary contract between code units
- Projects without binary compatibility commitments **must** mark ABI as "not applicable" — never invent it

**💡 Innovation:** Decouples "template completeness" from "factual accuracy." Templates can have empty fields, but empty fields must not pretend to have content. When agents reason from BASE.md, they see facts, not hallucinations.

---

### 5. agents/TODO.md — Append-Only Task Ledger 📝

**Traditional approach:** Agent finishes a task, context refreshes, and everything it did is lost.

**Agent Chassis approach:**

TODO.md is an **append-only** audit log. After completing a task, the agent **must** record: task description, evidence location, execution results, verification status. Old entries **must never** be deleted — even if a task was wrong, it can only be marked `CANCELLED` and a new entry created.

Format is also mandatory:

- Status labels: `NEW` / `ACTIVE` / `BLOCKED` / `COMPLETED` / `FAILED` / `CANCELLED`
- Every task must have: agent type, priority, scope, evidence source
- Subtasks must be checklist-ified

**💡 Innovation:** Agent behavior becomes auditable. *"If it isn't in TODO.md, it didn't happen."*

---

### 6. doc/DOCUMENTATION.md — User Manual That Doesn't Redefine the Project 📖

**Traditional approach:** User docs and project facts are disconnected. The manual says there's an API that the code hasn't implemented yet.

**Agent Chassis approach:**

DOCUMENTATION.md is the formal user manual, but it **must not redefine project facts**. If the manual conflicts with public entries, current facts, or the first five controlled documents, **fix the manual** — never use the manual to override facts.

Its content is constrained by AGENTS.md and RULES.md:

- Can only explain **released, verifiable** capabilities
- Cannot invent entries for template completeness
- Large-scale rewrites can **only** be triggered by `Run Documentation Generation`
- Small-scope syncs can only modify directly related text within authorized scope

**💡 Innovation:** User documentation is explicitly constrained as a "downstream of facts" — not "another independent narrative."

---

## Overall Innovation Summary 🎯

| Design | Traditional Approach | Agent Chassis |
| --- | --- | --- |
| Document Organization | One giant prompt blob | Six controlled documents with isolated responsibilities |
| Conflict Resolution | No rules, model guesses | `README > AGENTS > RULES > BASE > TODO > DOCUMENTATION` |
| Execution Trigger | "Please help me check this" | Hard command switches like `Run Diff Review` with prefix-chain gates |
| Subagent Permissions | No read/write distinction | `explore` / `general` types bound to access boundaries |
| Rule Protection | None | Chapter 13 anti-weakening gate: "must" cannot become "should" |
| Version Management | Each doc on its own | All six documents **must** increment in sync, identical versions |
| Fact Boundaries | Template fabricates filler | `not applicable` and `not established` are valid values |
| Task Tracking | Lost in context refresh | TODO.md append-only, audit trail permanently preserved |
| User Docs | Independent narrative | Constrained by first five documents, cannot override facts |

---

## Use Cases 🚀

- Engineering teams that need a unified project entry, fact baseline, engineering rules, follow-up plan, and user manual
- Collaborative projects where developers and agents must share the same constraint set
- Long-lived maintenance projects that need to separate current facts from future plans
- Projects with clear public entries (API, CLI, SDK, services, etc.) where entries must stay consistent with code facts

---

## Quick Start ⚡

If you want an agent to instantiate the templates for a real project, copy the six controlled documents first, then paste the text from `BOOTSTRAP.md` into the AI Agent chat. `BOOTSTRAP.md` itself is not copied into the target project.

```bash
# 1. Copy the six documents into your project root
git clone https://github.com/yourname/agent-chassis.git

# 2. Globally replace all {{%...%}} placeholders
#    PROJECT_NAME → your project name
#    DOCUMENT_VERSION → initial version (e.g., v0.1)
#    Fill the rest as needed

# 3. Point CodexCLI at it
codex --instructions AGENTS.md

# 4. Start working. The agent reads AGENTS.md first, then RULES, BASE, TODO by responsibility, and writes DOCUMENTATION only when needed.
```

---

## Design Principles 🏗️

- **Constraints over suggestions.** "Must" stays "must." 🔒
- **Isolation over mixing.** Six documents, six jobs. 📦
- **Chains over chaos.** Prefix gates enforce order. ⛓️
- **Placeholders over fabrication.** `{{%...%}}` means "you fill this in" — not "I'll make something up." 🎯

---

*Built for people who are tired of context drift.* 🏹
