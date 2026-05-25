# {{%PROJECT_NAME}} Project Guide

## 1. Version Information

- Current version: `{{%DOCUMENT_VERSION}}`
- Updated: {{%UPDATED_DATE}}
- Synchronized documents: `README.md {{%DOCUMENT_VERSION}}`, `AGENTS.md {{%DOCUMENT_VERSION}}`, `agents/RULES.md {{%DOCUMENT_VERSION}}`, `agents/BASE.md {{%DOCUMENT_VERSION}}`, `agents/TODO.md {{%DOCUMENT_VERSION}}`, `doc/DOCUMENTATION.md {{%DOCUMENT_VERSION}}`

## 2. Document Role

`README.md` is the top-level entry document for {{%PROJECT_NAME}}. It is written for project users, developers, and maintainers, and answers "what is this project, and where should I start?" This document carries the project summary, capability boundary summary, usage entry points, document navigation, and document priority.

This document does not carry agent execution rules, detailed engineering rules, the full factual baseline, follow-up plans, known issue records, or formal user manual content. Agent execution rules are defined in `AGENTS.md`; engineering rules and automatic quality guard rules shared by developers and agents are defined in `agents/RULES.md`; the current factual baseline is defined in `agents/BASE.md`; follow-up plans and known issues are defined in `agents/TODO.md`; the formal user manual is defined in `doc/DOCUMENTATION.md`.

`{{%...}}` marks a template field. After this template is instantiated for a real project, every placeholder must be replaced, removed, or explicitly marked as not applicable. Published documents must not retain unexplained placeholders.

## 3. Project Summary

{{%PROJECT_NAME}} is a {{%PROJECT_TYPE}} for {{%PROJECT_DOMAIN}} scenarios. The concrete delivery model, runtime environment, public entries, user roles, and capability range must be filled by the instantiated project in `agents/BASE.md` and summarized here.

A public entry is any user-visible, user-obtainable, and user-verifiable API, CLI, SDK, service, plugin, protocol, configuration, user interface, data format, model entry, deployment entry, operations entry, or documentation entry. An API is a usage contract between users and code, system interfaces, or programmatic entries; it is one kind of public entry. An ABI is a binary contract between code units and applies only when the project has exported symbols, calling conventions, type layouts, link artifacts, or binary compatibility commitments. Do not collapse all public entries into API, do not confuse API with ABI, and do not invent ABI boundaries for projects without binary compatibility commitments.

## 4. Capability Boundary Summary

- Current project facts, directory responsibilities, build and installation status, test entries, and capability status are governed by `agents/BASE.md`.
- Released capabilities, preview capabilities, internal capabilities, placeholder capabilities, and uncommitted capabilities must be recorded separately. Incomplete, skeletal, internal-only, or unpublished capabilities must not be described as released capabilities.
- Public entries must match the real delivery model. Nonexistent API, CLI, SDK, service, plugin, protocol, configuration, user interface, data format, model entry, deployment entry, operations entry, or documentation entry must be marked as not applicable or removed. Do not invent entries for template completeness.
- The formal user manual only explains how users can use capabilities that are already public, obtainable, and verifiable. If the manual conflicts with public entries, current facts, or the first five controlled documents, revise the manual instead of using it to redefine project facts.

## 5. Usage Entries

| Entry type | Entry location | Audience | Description |
| --- | --- | --- | --- |
| Primary public entry | `{{%PRIMARY_PUBLIC_ENTRY}}` | {{%PRIMARY_USER_ROLE}} | {{%PRIMARY_PUBLIC_ENTRY_DESCRIPTION}} |
| Authoritative public-entry fact source | `{{%PUBLIC_ENTRY_AUTHORITY}}` | {{%MAINTAINER_ROLE}} | Current source used to confirm public entries, capability boundaries, and compatibility commitments. |
| Build or generation entry | `{{%BUILD_ENTRY}}` | {{%BUILD_MAINTAINER_ROLE}} | {{%BUILD_ENTRY_DESCRIPTION}} |
| Test or verification entry | `{{%TEST_ENTRY}}` | {{%VERIFICATION_MAINTAINER_ROLE}} | {{%TEST_ENTRY_DESCRIPTION}} |
| Installation or release entry | `{{%INSTALL_OR_RELEASE_ENTRY}}` | {{%RELEASE_MAINTAINER_ROLE}} | {{%INSTALL_OR_RELEASE_DESCRIPTION}} |
| Formal user manual | `doc/DOCUMENTATION.md` | {{%END_USER_ROLE}} | Explains released and usable capabilities for published users. |

## 6. Document Navigation and Priority

| Priority | Document | Core function | Progression |
| --- | --- | --- | --- |
| 1 | `README.md` | Project entry, project summary, capability boundary summary, usage entries, document navigation | Highest-level entry document; answers "what is this project, and where should I start?" |
| 2 | `AGENTS.md` | Agent control entry, loading rules, version synchronization, document priority, minimum context | Defines how agents read, execute, synchronize, and maintain the project based on README navigation. |
| 3 | `agents/RULES.md` | Engineering rules, public-entry and compatibility constraints, quality guard, tests, build, installation, document maintenance, user manual rules | Expands AGENTS-level red lines into executable engineering rules. |
| 4 | `agents/BASE.md` | Current factual baseline, directory responsibilities, public-entry facts, compatibility boundary facts, build and installation facts, test-entry facts, current capability status | Records the actual current project state under RULES constraints. |
| 5 | `agents/TODO.md` | Follow-up plans, known issues, priorities, evidence locations, first actions, verification suggestions | Derives what should be fixed next from BASE facts and verified findings. |
| 6 | `doc/DOCUMENTATION.md` | Formal user manual for published users | Explains how final users use released and available capabilities based on public entries and stable current facts. |

Progression:

```text
README.md
  -> Project entry and navigation
AGENTS.md
  -> Agent behavior, loading rules, version synchronization
agents/RULES.md
  -> Engineering rules, non-breakable constraints, automatic quality guard, user manual rules
agents/BASE.md
  -> Current project factual baseline
agents/TODO.md
  -> Follow-up plans based on factual gaps and confirmed issues
doc/DOCUMENTATION.md
  -> Formal user manual for published users
```

In short: `README` defines the entry, `AGENTS` defines agent rules, `RULES` defines engineering constraints and quality guard, `BASE` defines current facts, `TODO` defines follow-up actions and known issues, and `DOCUMENTATION` defines the published user manual.

Agents automatically run the quality guard appropriate to the risk of each change. Later quality activities depend on earlier checks; if an earlier check is incomplete, failed, blocked, interrupted by hard limits, or waiting for user judgment, later quality activities must not start. Multi-agent orchestration, `explore`/`general` subagent type assignment, queueing, stop-and-resume behavior, reports, acceptance, and TODO boundaries are governed by `AGENTS.md` and `agents/RULES.md`.

## 7. Suitable Use Cases

- Engineering projects that need unified project entry, factual baseline, engineering rules, follow-up plan, and user manual.
- Collaborative projects where developers and agents must share engineering rules, document boundaries, factual boundaries, and verification rules.
- Long-lived maintenance projects that need to separate current facts, follow-up plans, automatic quality guard, user manuals, and internal maintenance rules.
- Projects that must record API, CLI, SDK, service, plugin, protocol, configuration, user interface, data format, model entry, deployment entry, operations entry, and documentation entry according to the real delivery model.

## 8. Instantiation Checklist

- [ ] Replace or remove every `{{%...}}` placeholder. Mark uncertain facts as `not established` or `not applicable`.
- [ ] Fill in project type, target users, delivery model, public entries, and usage entries.
- [ ] Establish the current factual baseline in `agents/BASE.md`; do not treat reserved template fields as project facts.
- [ ] Define quality guard, compatibility boundaries, and text-format requirements in `agents/RULES.md`.
- [ ] Record evidence-backed known issues and follow-up plans in `agents/TODO.md`; keep `No confirmed items` when there are no confirmed issues.
- [ ] Write the formal user manual in `doc/DOCUMENTATION.md` and trim non-applicable sections according to the public-entry matrix.
