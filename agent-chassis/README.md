# `{{%PROJECT_NAME}}` Project Description

## 1. Version Information

- Current version: `{{%DOCUMENT_VERSION}}`
- Updated: `{{%UPDATED_DATE}}`
- Synchronized documents: `README.md {{%DOCUMENT_VERSION}}`, `AGENTS.md {{%DOCUMENT_VERSION}}`, `agents/RULES.md {{%DOCUMENT_VERSION}}`, `agents/BASE.md {{%DOCUMENT_VERSION}}`, `agents/TODO.md {{%DOCUMENT_VERSION}}`, `doc/DOCUMENTATION.md {{%DOCUMENT_VERSION}}`

## 2. Document Role

`README.md` is the top-level entry document for `{{%PROJECT_NAME}}`, written for project users, developers, and maintainers. It answers "what is this project, and where should I start?" This document carries the project summary, capability boundary summary, usage entries, document navigation, and document priority.

This document does not carry agent execution rules, detailed engineering rules, the complete factual baseline, follow-up implementation plans, known issue records, or the formal user manual. Agent execution rules are defined in `AGENTS.md`; detailed engineering rules, coding style, automatic quality guard, unobtrusive quality guard, document quality domain, and user manual writing rules shared by developers and agents are defined in `agents/RULES.md`; the current factual baseline is defined in `agents/BASE.md`; follow-up implementation plans and known issue records are defined in `agents/TODO.md`; the formal user manual is defined in `doc/DOCUMENTATION.md`.

`README.md`, `AGENTS.md`, and `agents/RULES.md` are project constraint documents. Ordinary agent iterations must not independently modify protected content; whether modification is allowed, how approval is obtained, and how verification is performed are governed by the complete gates in `AGENTS.md` and `agents/RULES.md`.

These limits do not extend to autonomous controlled iteration within the responsibilities of `agents/BASE.md`, `agents/TODO.md`, and `doc/DOCUMENTATION.md`; those files still record current facts, to-do plan content, and user manual content according to their own roles.

This document uses the brace-percent form to mark template fields. After instantiation into formal project documents, placeholders must be replaced, removed, or explicitly marked as not applicable. Formal release documents must not retain unexplained placeholders.

## 3. Project Summary

`{{%PROJECT_NAME}}` is a `{{%PROJECT_TYPE}}` for `{{%PROJECT_DOMAIN}}` scenarios. The primary delivery form, runtime environment, public entries, user roles, and capability scope are filled by the instantiated project in `agents/BASE.md` and summarized in this file.

A public entry is any user-visible, user-obtainable, and user-verifiable API, CLI, SDK, service, plugin, protocol, configuration, user interface, data format, model entry, deployment entry, operations entry, or documentation entry. An API is a usage contract between users and code, system interfaces, or programmatic entries; it is one kind or group of public entries. An ABI is a binary contract between code units and applies only when the project has exported symbols, calling conventions, type layouts, link artifacts, or binary compatibility commitments. Public entries must not all be collapsed into API, API and ABI must not be confused, and ABI boundaries must not be invented for projects without binary compatibility commitments.

## 4. Capability Boundary Summary

- Current project facts, directory responsibilities, build and installation status, test entries, and capability status are governed by `agents/BASE.md`.
- Released capabilities, preview capabilities, internal capabilities, placeholder capabilities, and uncommitted capabilities must be filled separately; ***unfinished, skeletal, internal-only, or unpublished capabilities must not be described as released capabilities***.
- Public entries may be API, CLI, SDK, service, plugin, protocol, configuration, user interface, data format, model entry, deployment entry, operations entry, documentation entry, or other user-visible entries; the instantiated project must fill them according to the real delivery form.
- User-facing usage instructions are governed by `doc/DOCUMENTATION.md`; if they conflict with public entries, current facts, or the first five engineering control documents, revise the manual instead of using the manual to redefine project facts.
- Automatic quality domains, gates, and workflows for complete generation or major rewrites of the formal user manual are governed by `AGENTS.md` and `agents/RULES.md`.

## 5. Usage Entries

| Entry type | Entry location | Audience | Description |
| --- | --- | --- | --- |
| Primary public entry | `{{%PRIMARY_PUBLIC_ENTRY}}` | `{{%PRIMARY_USER_ROLE}}` | `{{%PRIMARY_PUBLIC_ENTRY_DESCRIPTION}}` |
| Authoritative public-entry fact source | `{{%PUBLIC_ENTRY_AUTHORITY}}` | `{{%MAINTAINER_ROLE}}` | Used to confirm current facts for API, CLI, SDK, service, plugin, protocol, configuration, user interface, data format, model entry, deployment entry, operations entry, and documentation entry. |
| Build or generation entry | `{{%BUILD_ENTRY}}` | `{{%BUILD_MAINTAINER_ROLE}}` | `{{%BUILD_ENTRY_DESCRIPTION}}` |
| Test or verification entry | `{{%TEST_ENTRY}}` | `{{%VERIFICATION_MAINTAINER_ROLE}}` | `{{%TEST_ENTRY_DESCRIPTION}}` |
| Installation or release entry | `{{%INSTALL_OR_RELEASE_ENTRY}}` | `{{%RELEASE_MAINTAINER_ROLE}}` | `{{%INSTALL_OR_RELEASE_DESCRIPTION}}` |
| Formal user manual | `doc/DOCUMENTATION.md` | `{{%END_USER_ROLE}}` | Explains published and usable capabilities for release users; complete generation or major rewrites are governed by the automatic quality domains and gates in `AGENTS.md` and `agents/RULES.md`. |

Entries that do not exist in the instantiated project must be explicitly marked `not applicable` or removed from project facts. Do not invent a CLI, SDK, service, public header where applicable, installation package, test menu, or binary artifact merely for template completeness.

## 6. Document Navigation and Priority

| Priority | Document | Core function | Progression |
| --- | --- | --- | --- |
| 1 | `README.md` | Project entry, project summary, capability boundary summary, usage entries, document navigation | Highest-level entry document; answers "what is this project, and where should I start?" |
| 2 | `AGENTS.md` | Agent control entry, loading order, automatic quality guard, unobtrusive quality guard, hard write gate for project constraint documents, version synchronization, document priority, minimum context | Based on the navigation in `README.md`, defines how agents read, execute, synchronize, and maintain the project. |
| 3 | `agents/RULES.md` | Detailed engineering rules, coding style, public-entry and compatibility constraints, tests, build, installation, document maintenance, automatic quality guard, unobtrusive quality guard, document quality domain, and user manual writing rules | Expands the high-level red lines in `AGENTS.md` into executable engineering rules and answers "what must be followed when changing code or documents, running built-in quality control, or generating manuals?" |
| 4 | `agents/BASE.md` | Current factual baseline, directory responsibilities, public-entry facts, compatibility boundary facts, build and installation facts, test-entry facts, and current capability status | Records "what the project actually is now" under `agents/RULES.md` constraints. |
| 5 | `agents/TODO.md` | Follow-up implementation plans, known issues, priorities, evidence locations, first actions, verification suggestions | Derives "what should be added next, what should be done first, and which known issues need handling" from current facts in `agents/BASE.md` and verified findings. |
| 6 | `doc/DOCUMENTATION.md` | Formal user manual for release users | Based on public entries and current stable facts, explains to end users "how to use capabilities that are already public and usable" without carrying writing rules, internal processes, QA checklists, or maintenance rules. |

Progression summary:

- `README.md`: project entry and navigation.
- `AGENTS.md`: agent behavior, loading rules, and version synchronization.
- `agents/RULES.md`: engineering constraints, non-breakable constraints, automatic quality guard, unobtrusive quality guard, and user manual writing rules.
- `agents/BASE.md`: current project factual baseline.
- `agents/TODO.md`: follow-up plans formed from factual gaps and confirmed issues.
- `doc/DOCUMENTATION.md`: formal user manual for release users.

In short: `README.md` defines the entry, `AGENTS.md` defines agent rules, `agents/RULES.md` defines engineering constraints, automatic quality guard, and user manual writing rules, `agents/BASE.md` defines current facts, `agents/TODO.md` defines follow-up actions and known issues, and `doc/DOCUMENTATION.md` defines the release user manual.

Automatic quality guard navigation:

`README.md` only identifies where the automatic quality guard is defined. Quality control is embedded in the ordinary task lifecycle; users do not need to, and should not, operate the quality chain through standalone phrases. Detailed rules are governed by `AGENTS.md` and `agents/RULES.md`.

| Quality scope | Navigation target | `README.md` summary | Authoritative details |
| --- | --- | --- | --- |
| Lightweight automatic quality-control mode | `incremental difference domain`, `incremental security domain`, `factual boundary domain`, `document quality domain` | Automatically included when ordinary task risk is lower or the impact scope is clear. This file does not expand per-domain task briefs. | `AGENTS.md`; `agents/RULES.md` |
| Full automatic quality-control mode | `public impact domain`, `global security domain`, `static analysis domain`, `documentation release domain` | Automatically included when ordinary task risk is higher, impact scope is broader, or pre-freeze review is required. This file only provides navigation. | `AGENTS.md`; `agents/RULES.md` |
| Complex task planning discipline | underlying fact derivation, blocker clarification, plan readiness, and acceptance tie-back | Complex ordinary tasks first clarify key facts, constraints, and blockers, then form an executable plan. This file does not expand the internal state machine, quality-domain chains, or subagent task briefs. | `AGENTS.md`; `agents/RULES.md` |

## 7. Suitable Use Cases

- Engineering projects that need unified project entry, factual baseline, engineering rules, to-do plans, and user manual.
- Collaborative projects where developers and agents must share engineering rules, coding style, document boundaries, and verification rules.
- Long-lived maintenance projects that need to distinguish current facts, to-do plans, automatic quality guard, user manual, and internal maintenance rules.
- Projects that need to fill API, CLI, SDK, service, plugin, protocol, configuration, user interface, data format, model entry, deployment entry, operations entry, and documentation entry according to the real delivery form.

## Appendix

### Instantiation Checklist

This checklist is a representative template-stage checklist. During instantiation or later template maintenance, this file's full text **must first be scanned** for all valid `{{%...}}` placeholders and a deduplicated set must be established. This checklist ***must not replace*** full-file scan results. The ellipsis form `{{%...}}` does not count as a fill item when it is used only as syntax explanation. After instantiation is complete, this entire section and `### Placeholder Checklist` ***must be deleted*** and must not remain in formal output.

- Fill `README.md` identity information: project name, entry-document positioning, and applicable project name must match the current project.
- Fill the project summary: project domain, project type, primary delivery form, runtime environment, user roles, and capability scope summary must reflect the current project.
- Fill audience information: primary user role, end user role, and maintainer roles must match the audiences of this document.
- Fill public entries: primary public entry, primary public entry description, and authoritative public-entry fact source must come from the real delivery form described in this document; nonexistent entries must be marked `not applicable` in this document.
- Fill build, test, installation, or release entries: the corresponding entries, descriptions, and maintainer roles must be navigable and verifiable project entries in this document.
- Check the authoritative fact sources, document roles, and priority references in this document, and ensure they serve only the navigation and summary role of `README.md`.
- Fill all owner roles: maintainer role, build maintainer role, verification maintainer role, release maintainer role, and end user role must have clear responsibility separation.
- Fill version and date: current version, synchronized document version references, and updated date must be consistent.

### Placeholder Checklist

This checklist lists **at most 10 items** of representative or key placeholders or categories. The full handling scope is governed by full-file scan results for valid `{{%...}}` placeholders. When any placeholder is added, deleted, or renamed, handling rules **must be updated** according to scan results. The items below ***must not be maintained alone***.

- Metadata: `{{%PROJECT_NAME}}`, `{{%DOCUMENT_VERSION}}`, `{{%UPDATED_DATE}}` in YYYY-MM-DD format
- Project positioning: `{{%PROJECT_DOMAIN}}`, `{{%PROJECT_TYPE}}`
- Public entry: `{{%PRIMARY_PUBLIC_ENTRY}}`, `{{%PRIMARY_PUBLIC_ENTRY_DESCRIPTION}}`
- Public fact source: `{{%PUBLIC_ENTRY_AUTHORITY}}`
- User roles: `{{%PRIMARY_USER_ROLE}}`, `{{%END_USER_ROLE}}`
- Maintainer role: `{{%MAINTAINER_ROLE}}`
- Build entry: `{{%BUILD_ENTRY}}`, `{{%BUILD_ENTRY_DESCRIPTION}}`
- Test entry: `{{%TEST_ENTRY}}`, `{{%TEST_ENTRY_DESCRIPTION}}`
- Installation or release entry: `{{%INSTALL_OR_RELEASE_ENTRY}}`, `{{%INSTALL_OR_RELEASE_DESCRIPTION}}`
- Build, verification, and release maintainer roles: `{{%BUILD_MAINTAINER_ROLE}}`, `{{%VERIFICATION_MAINTAINER_ROLE}}`, `{{%RELEASE_MAINTAINER_ROLE}}`
