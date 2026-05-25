# {{%PROJECT_NAME}} Agent Execution Rules

## 1. Version Information

- Current version: `{{%DOCUMENT_VERSION}}`
- Updated: {{%UPDATED_DATE}}
- Synchronized documents: `README.md {{%DOCUMENT_VERSION}}`, `AGENTS.md {{%DOCUMENT_VERSION}}`, `agents/RULES.md {{%DOCUMENT_VERSION}}`, `agents/BASE.md {{%DOCUMENT_VERSION}}`, `agents/TODO.md {{%DOCUMENT_VERSION}}`, `doc/DOCUMENTATION.md {{%DOCUMENT_VERSION}}`
- Fixed protocol fields: `README.md`, `AGENTS.md`, `agents/RULES.md`, `agents/BASE.md`, `agents/TODO.md`, `doc/DOCUMENTATION.md`, `test build rules`, `explore`, and `general` are protocol constants of this document-maintenance framework. They must be used exactly as written and must not be replaced by placeholders, renamed, translated, split, or merged.

## 2. Document Role

`AGENTS.md` is the agent execution rulebook for {{%PROJECT_NAME}}. It is written for agents participating in the project and carries loading order, version synchronization, document priority, automatic quality guard entry, minimum context, and non-ignorable high-level red lines.

This document does not expand detailed engineering rules, coding style constraints, the full factual baseline, follow-up plans, quality-guard details, or user manual writing rules. Detailed engineering rules, automatic quality-guard workflows, and user manual writing rules shared by developers and agents are defined in `agents/RULES.md`; `agents/RULES.md` is not an agent-private prompt, but an engineering constraint shared by humans and agents. Project entry and navigation are governed by `README.md`; the factual baseline is governed by `agents/BASE.md`; follow-up plans and known issues are governed by `agents/TODO.md`; the formal user manual is governed by `doc/DOCUMENTATION.md`.

## 3. Document Priority

When the six documents conflict, resolve the conflict by responsibility:

1. Conflicts about project entry, project summary, and document navigation are governed by `README.md`.
2. Conflicts about agent behavior, loading order, version synchronization, automatic quality guard entry, and document priority are governed by `AGENTS.md`.
3. Conflicts about engineering rules, coding style, public entries, API/interface boundaries, compatibility boundaries, tests, build, installation, document maintenance, quality-guard details, and user manual writing rules are governed by `agents/RULES.md`.
4. Conflicts about current facts, directory responsibilities, build and installation, test entries, and capability status are governed by `agents/BASE.md`.
5. Conflicts about TODO priority, known issues, follow-up plans, evidence locations, first actions, and verification suggestions are governed by `agents/TODO.md`.
6. When user manual content conflicts with project facts, the conflicting content must not redefine project facts. `doc/DOCUMENTATION.md` must be corrected by public entries and stable current facts from the first five documents.

## 4. Loading Rules

- If a task touches source code, public entries, APIs/interfaces, build, tests, installation, directory responsibilities, algorithm implementation, performance paths, compatibility boundaries, quality guard, or manual output, the agent must read `agents/RULES.md`.
- If a task involves project-fact judgment, especially source code, public entries, APIs/interfaces, build, test entries, installation artifacts, or current capability status, the agent must read `agents/BASE.md` as needed.
- If a task adds, removes, closes, or reorders follow-up capabilities or known issues, the agent must read `agents/TODO.md` as needed.
- If a task involves formal user-facing instructions, external user manuals, public entry-group explanations, or user examples, the agent must read `doc/DOCUMENTATION.md`, `{{%PRIMARY_PUBLIC_ENTRY}}`, and `{{%PUBLIC_ENTRY_AUTHORITY}}` as needed according to the primary public entry and fact source recorded in `agents/BASE.md`.
- Small text replies that do not depend on project facts do not need to mechanically read every document.

## 5. Automatic Quality Guard

- Read receipt: whenever an agent actually reads this `AGENTS.md`, whether or not the user asked for it, the next visible response must state the current version found and briefly summarize this file.
- Loading check: whenever the user message contains the complete literal phrase `test build rules`, the agent must directly reply with the current version found and a summary of this file. The agent must not run tools and must not misread the request as a build, test, or code-modification request.
- During every iteration, the agent must automatically run the necessary quality guard according to change risk. The quality guard does not depend on manual user triggers and must not require the user to remember or type internal task names.
- Routine lightweight changes must at least cover incremental differences, obvious security regressions, factual boundaries, and controlled-document consistency. Changes involving public entries, compatibility boundaries, cross-module logic, security surface, static coverage, or formal manual content must escalate to the full guard.
- Later quality activities depend on earlier check results. If an earlier check is incomplete, failed, blocked, interrupted by hard limits, or waiting for user judgment, later quality activities must not start.
- Every quality stage must have an independent task brief, subagent orchestration, report, acceptance step, and TODO-candidate boundary. Conclusions from one stage must not replace the main inspection, summary, review, or acceptance of a later stage.
- Capability detection, three-layer or two-layer subagent architecture, prohibition on proactive downgrade, queueing when concurrency is insufficient, stop-and-resume when hard limits are reached, phased downgrade only when no subagent capability exists, independent reports, and TODO recording boundaries are strong constraints.
- Subagent type selection must be bound to access boundaries: read-only checks, exploration, inventory building, fact verification, summary, and review tasks must use `explore`; any task that modifies the worktree, writes `agents/TODO.md`, synchronizes version metadata, generates drafts, merges drafts, or revises formal documents must use `general`; mixed read/write tasks must be split.
- A parent agent, coordinator, or session agent must not privately cancel, terminate, replace, merge, or declare a subagent failed merely because the subagent is taking time, has no temporary output, is slow, is queued, or is handling a complex task. An unfinished subagent may end only when the user explicitly cancels, a platform or tool hard limit forces interruption, the subagent itself returns completion/failure/blockage, or continuing would create unacceptable risk.
- Issues found by the automatic quality guard must not be resolved by unauthorized changes to source code, public headers where applicable, build scripts, test entries, installation logic, or compatibility boundaries. Documentation public entries may be narrowly and lawfully revised only within the authorized scope, and such revision must not change code facts or invent public capabilities.
- Confirmed issues that have an evidence location, impact scope, and suggested action and require follow-up handling must be submitted to `agents/TODO.md`. Low-confidence findings, tool uncertainty, unlocated guesses, and pure tool noise must remain only in the report.

## 6. Version Synchronization and Document Maintenance

- When any of the six controlled documents is modified, the responsible scope, cross-references, and version synchronization state must be checked.
- After modification, the versions of all six controlled documents must be incremented in sync and kept identical. The version format is `vMajor.Minor`; the minor number increments by decimal `1`; the major number increments when document structure, role boundaries, or non-breakable constraints are added, removed, or materially changed.
- When source code, public entries, APIs/interfaces, build scripts, test entries, installation logic, directory responsibilities, or current capability status change, `agents/BASE.md` must be checked in sync.
- When code-fact changes require controlled-document updates, the relevant facts, boundaries, indexes, or TODO information must be updated according to document responsibility. If the code-fact change directly affects descriptions of released capabilities in the formal user manual, only directly related small-scope text, table rows, notes, example signatures, version metadata, or local index items in `doc/DOCUMENTATION.md` may be synchronized. This must not be interpreted as permission to fully generate, heavily rewrite, reorder the whole manual, or refresh public-entry descriptions systemically.
- When follow-up capabilities or known issues are added, removed, closed, or reordered, `agents/TODO.md` must be checked in sync.
- When external user manual content changes, the document index in `README.md` and factual scope in `agents/BASE.md` must be checked in sync.
- After each controlled-document change, grammar, syntax, wording errors, and ambiguous expressions must be checked. Redundancy may be refined only while facts, meaning, constraint strength, and behavioral boundaries remain unchanged; true constraints must not be removed, weakened, or blurred for brevity.
- After each code or document change, modified text files must be checked according to the text-format and Markdown validation rules in `agents/RULES.md`, including line endings, encoding, EOF newline, trailing whitespace removal, and syntax. Markdown files must run markdownlint or an equivalent syntax check and fix issues.

## 7. Minimum Project Context

The project type, delivery model, primary language or runtime, public entries, build entry, test entry, installation artifacts, capability domains, compatibility model, and user manual scope for {{%PROJECT_NAME}} must be filled by the instantiated project in `agents/BASE.md`. This section keeps only the minimum summary and must not make any technology stack, build system, public header where applicable, CLI, server, frontend, SDK, model, or documentation project form the default for all projects.

A public entry is any user-visible, user-obtainable, and user-verifiable API, CLI, SDK, service, plugin, protocol, configuration, user interface, data format, model entry, deployment entry, operations entry, or documentation entry. An API is a usage contract between users and code, system interfaces, or programmatic entries; it is one kind of public entry. An ABI is a binary contract between code units and applies only when the project has exported symbols, calling conventions, type layouts, link artifacts, or binary compatibility commitments. If the project has no ABI commitment, the quality guard and user manual must mark ABI as not applicable and must not invent binary compatibility boundaries.

Minimum context for the instantiated project:

| Item | Content |
| --- | --- |
| Project type | {{%PROJECT_TYPE}} |
| Primary delivery model | {{%PRIMARY_DELIVERY_MODEL}} |
| Primary public entry | `{{%PRIMARY_PUBLIC_ENTRY}}` |
| Authoritative public-entry fact source | `{{%PUBLIC_ENTRY_AUTHORITY}}` |
| Build entry | `{{%BUILD_ENTRY}}` |
| Test entry | `{{%TEST_ENTRY}}` |
| Installation or release entry | `{{%INSTALL_OR_RELEASE_ENTRY}}` |
| Compatibility model | {{%COMPATIBILITY_MODEL}} |

## 8. High-Level Red Lines

- Do not break commitments already made through API, CLI, SDK, service, plugin, protocol, configuration, user interface, data format, model entry, deployment entry, operations entry, or documentation entry. Projects with ABI commitments must also not break exported symbols, calling conventions, type layouts, link artifacts, or binary compatibility boundaries. ABI compatibility judgment must focus on binary boundaries between code units; API and ABI must not be conflated.
- Do not bypass or weaken constraints in `agents/RULES.md` about change boundaries, worktree protection, hot paths, state management, tests, full validation, automatic quality guard, subagent lifecycle discipline, `explore`/`general` subagent type assignment, or user manual writing rules.
- Do not claim support for platforms, runtimes, hardware backends, algorithmic capabilities, service capabilities, interface capabilities, or release capabilities that are not implemented, authorized, or verified.
- Do not expand technology-stack constraints from one project type into defaults for all projects. C/C++, DSP, CMake, binary ABI, SIMD, GPU, server-side, frontend, model, and documentation-project-specific rules may be enabled only when their applicability conditions are met.
