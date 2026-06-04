# `{{%PROJECT_NAME}}` Development Baseline

## 1. Version Information

- Current version: `{{%DOCUMENT_VERSION}}`
- Updated: `{{%UPDATED_DATE}}`
- Synchronized documents: `README.md` (`{{%DOCUMENT_VERSION}}`), `AGENTS.md` (`{{%DOCUMENT_VERSION}}`), `agents/RULES.md` (`{{%DOCUMENT_VERSION}}`), `agents/BASE.md` (`{{%DOCUMENT_VERSION}}`), `agents/TODO.md` (`{{%DOCUMENT_VERSION}}`), `doc/DOCUMENTATION.md` (`{{%DOCUMENT_VERSION}}`)
- Factual scope: `{{%PRIMARY_PUBLIC_ENTRY}}`, `{{%PUBLIC_ENTRY_AUTHORITY}}`, `{{%SOURCE_OR_CONTENT_ROOT}}`, `{{%RUNTIME_ENTRY}}`, `{{%BUILD_ENTRY}}`, `{{%TEST_ENTRY}}`, `{{%INSTALL_OR_RELEASE_ENTRY}}`, `README.md`, `AGENTS.md`, `agents/RULES.md`, `agents/TODO.md`, `doc/DOCUMENTATION.md`

## 2. Document Role

`agents/BASE.md` is the project factual baseline. It carries the current project positioning, delivery form, public entries, compatibility boundaries, directory responsibilities, build and installation facts, test-entry facts, and current capability status.

This file does not carry agent control rules, detailed engineering rules, automatic quality guard details, user manual writing rules, the formal user manual, follow-up implementation plans, or known issue records. It records only rule ownership and factual maintenance relationships. The authoritative locations for corresponding facts are: `AGENTS.md` for agent control entry, `agents/RULES.md` for detailed engineering rules, automatic quality guard, and user manual writing rules, `README.md` for project summary, `agents/TODO.md` for follow-up plans and known issues, and `doc/DOCUMENTATION.md` for the formal user manual.

When source code, public entries, API/interface boundaries, build scripts, test entries, installation logic, directory responsibilities, or current capability status change as facts, this file **records only the current facts within this file's responsibility**. Cross-document version synchronization, automatic quality guard, and user manual output processes are maintained by `AGENTS.md` and `agents/RULES.md`. Confirmed factual gaps and known issues are carried by `agents/TODO.md`.

Current controlled-rule facts are: Chapter 10 of `agents/RULES.md` maintains build and installation, document maintenance, automatic quality guard, underlying fact derivation, task risk level, automatic quality-loop level, text-format validation, and verification boundaries; Chapter 11 maintains lightweight automatic quality-control rules; Chapter 12 maintains full automatic quality-control rules; Chapter 13 maintains formal user manual writing rules, templates, confidentiality boundaries, and checklists. The complete list of fixed protocol constants, automatic quality guard summary, and execution details are defined in `AGENTS.md` / `agents/RULES.md`; this file only references the existence and ownership of these rules and ***does not copy*** their executable protocols.

## 3. Automatic Quality-Guard Rule Ownership

The automatic quality guard, as a controlled-rule fact, belongs to `AGENTS.md` and `agents/RULES.md`. This file only records its factual baseline relationship and ***must not copy*** per-quality-domain task briefs, subagent lifecycles, or formal manual output details.

- Automatic quality-domain chain: The quality-domain lists, serial order, and execution details of the lightweight/full automatic quality-control groups are governed by `AGENTS.md` and `agents/RULES.md`; this file records only rule ownership and factual maintenance relationships.
- Underlying fact derivation: Fact/assumption/experience-based solution/preference distinction, blocker handling, plan-readiness gates, and acceptance tie-back for complex ordinary tasks are governed by `AGENTS.md` and `agents/RULES.md`; this file records only capability ownership and does not copy the state machine or execution protocol.
- Automatic quality loop: task risk levels, automatic quality-loop level, plan fields, chain-level stops, acceptance outputs, and to-do plan recording criteria are governed by `AGENTS.md` and `agents/RULES.md`; this file records only rule ownership and does not copy the judgment matrix or execution protocol.
- Factual maintenance relationship: When the automatic quality-domain chain, quality-domain orchestration rules, automatic quality-loop rules, `explore` / `general` or equivalent capability type ownership, task dependency graph, read/write ownership, to-do plan thresholds, or formal user manual output boundaries change as facts, this file only records rule ownership and current factual impact. Detailed execution authority remains in the automatic quality guard chapter of `AGENTS.md` and Chapters 10-13 of `agents/RULES.md`.

## 4. Project Positioning

`{{%PROJECT_NAME}}` is a `{{%PROJECT_TYPE}}` in the `{{%PROJECT_DOMAIN}}` domain, with `{{%PRIMARY_DELIVERY_FORM}}` as its primary delivery form. The project may be a local library, server application, CLI tool, frontend application, SDK, plugin, model, data engineering project, documentation engineering project, or another engineering form. During instantiation, it **must be filled according to the real project** and non-applicable technology-stack assumptions ***must not be inherited***.

Current positioning table:

| Item | Content |
| --- | --- |
| Project type | `{{%PROJECT_TYPE}}` |
| Project domain | `{{%PROJECT_DOMAIN}}` |
| Primary language or runtime | `{{%PRIMARY_LANGUAGE_OR_RUNTIME}}` |
| Primary delivery form | `{{%PRIMARY_DELIVERY_FORM}}` |
| Primary user role | `{{%PRIMARY_USER_ROLE}}` |
| Primary maintainer role | `{{%PRIMARY_MAINTAINER_ROLE}}` |
| Release scope | `{{%RELEASE_SCOPE}}` |

A public entry is any user-visible, user-obtainable, and user-verifiable API, CLI, SDK, service, plugin, protocol, configuration, user interface, data format, model entry, deployment entry, operations entry, or documentation entry. When a project has an API, the API is a usage contract between users and code, system interfaces, or programmatic entries, describing how users understand, call, and combine public capabilities. When a project has an ABI commitment, the ABI is a binary contract between code units, describing exported symbols, calling conventions, type layouts, link artifacts, and binary compatibility boundaries. Projects without a binary compatibility model must mark ABI as `not applicable` and must not invent ABI facts.

## 5. Public Entry and Compatibility Facts

Public-entry facts are filled by the instantiated project. Public entries may be API, CLI, SDK, service, plugin, protocol, configuration, user interface, data format, model entry, deployment entry, operations entry, or documentation entry. Nonexistent entries **must be marked** `not applicable`.
API, ABI, CLI, SDK, service, plugin, protocol, configuration, user interface, data format, model entry, deployment entry, operations entry, documentation entry, public header where applicable, public schema, protocol document, configuration description, binary library, test menu, and build script **must all be filled according to real project facts**. When not applicable, write `not applicable`; ***do not write any one project form as a universal default fact***.

| Public entry category | Entry location or identifier | Stability level | User responsibility | Project responsibility | Notes |
| --- | --- | --- | --- | --- | --- |
| `{{%PUBLIC_ENTRY_CATEGORY}}` | `{{%PUBLIC_ENTRY_LOCATION_OR_IDENTIFIER}}` | `{{%STABILITY_LEVEL}}` | `{{%USER_RESPONSIBILITY}}` | `{{%PROJECT_RESPONSIBILITY}}` | `{{%NOTES}}` |

Authoritative public-entry fact sources must be recorded separately. A source may be a public declaration file, OpenAPI or protocol schema, CLI help, SDK package metadata, user documentation, plugin list, configuration description, interface entry, data format description, model entry description, deployment description, operations description, or equivalent public material. When no verifiable source exists, write `not established`; do not infer public capabilities from reserved template fields.

| Fact source category | Location or identifier | Covered entry | Confidence | Notes |
| --- | --- | --- | --- | --- |
| `{{%PUBLIC_ENTRY_FACT_SOURCE_CATEGORY}}` | `{{%PUBLIC_ENTRY_AUTHORITY}}` | `{{%COVERED_PUBLIC_ENTRY}}` | `{{%FACT_SOURCE_CONFIDENCE}}` | `{{%FACT_SOURCE_NOTES}}` |

Compatibility boundaries are filled by the instantiated project.

| Compatibility category | Applicable | Current fact | Verification entry | Change risk |
| --- | --- | --- | --- | --- |
| API | `{{%API_APPLICABLE}}` | `{{%API_CURRENT_FACT}}` | `{{%API_VERIFICATION_ENTRY}}` | `{{%API_CHANGE_RISK}}` |
| ABI | `{{%ABI_APPLICABLE}}` | `{{%ABI_CURRENT_FACT}}` | `{{%ABI_VERIFICATION_ENTRY}}` | `{{%ABI_CHANGE_RISK}}` |
| Data format | `{{%DATA_FORMAT_APPLICABLE}}` | `{{%DATA_FORMAT_CURRENT_FACT}}` | `{{%DATA_FORMAT_VERIFICATION_ENTRY}}` | `{{%DATA_FORMAT_CHANGE_RISK}}` |
| Configuration format | `{{%CONFIG_FORMAT_APPLICABLE}}` | `{{%CONFIG_FORMAT_CURRENT_FACT}}` | `{{%CONFIG_FORMAT_VERIFICATION_ENTRY}}` | `{{%CONFIG_FORMAT_CHANGE_RISK}}` |
| Protocol or service contract | `{{%PROTOCOL_APPLICABLE}}` | `{{%PROTOCOL_CURRENT_FACT}}` | `{{%PROTOCOL_VERIFICATION_ENTRY}}` | `{{%PROTOCOL_CHANGE_RISK}}` |

If the project is a C/C++ local library, binary-compatibility-sensitive project, numerical hot-path project, DSP project, or specific-build-system project, corresponding conditional extension blocks in `agents/RULES.md` must be filled and executed. These facts must not be automatically applied to projects without the corresponding technology stack.

## 6. Directory Responsibility Facts

| Path | Current responsibility | External stability | Fact notes |
| --- | --- | --- | --- |
| `{{%DIRECTORY_PATH}}` | `{{%DIRECTORY_RESPONSIBILITY}}` | `{{%EXTERNAL_STABILITY}}` | `{{%FACT_NOTES}}` |

Directory responsibilities must distinguish public entries, internal implementation, test entries, build entries, generated directories, installation artifacts, third-party dependencies, document directories, and tool configuration directories. Non-public directories must not be written into the user manual as stable usage entries. Generated directories, cache directories, and temporary directories must not be written as factual authorities.

If the project contains third-party, vendored, or independent dependencies, their boundaries, licenses or reference sources, modification permissions, whether they are handled by interface-level coverage, and whether they participate in release artifacts should be marked in the table. If the project has no corresponding directory, fill `not applicable`; do not retain vague paths.

## 7. Build and Installation Facts

| Build or release item | Current fact | Entry location | Verification method | Notes |
| --- | --- | --- | --- | --- |
| Build system | `{{%BUILD_SYSTEM}}` | `{{%BUILD_ENTRY}}` | `{{%BUILD_VERIFICATION_METHOD}}` | `{{%NOTES}}` |
| Build configuration | `{{%BUILD_CONFIGURATION_MATRIX}}` | `{{%BUILD_CONFIGURATION_ENTRY}}` | `{{%BUILD_CONFIGURATION_VERIFICATION_METHOD}}` | `{{%NOTES}}` |
| Installation artifact | `{{%INSTALLATION_ARTIFACT}}` | `{{%INSTALL_OR_RELEASE_ENTRY}}` | `{{%INSTALLATION_VERIFICATION_METHOD}}` | `{{%NOTES}}` |
| Release package structure | `{{%RELEASE_PACKAGE_STRUCTURE}}` | `{{%RELEASE_PACKAGE_ENTRY}}` | `{{%RELEASE_PACKAGE_VERIFICATION_METHOD}}` | `{{%NOTES}}` |
| Resource or metadata | `{{%RESOURCE_OR_METADATA}}` | `{{%RESOURCE_GENERATION_ENTRY}}` | `{{%RESOURCE_VERIFICATION_METHOD}}` | `{{%NOTES}}` |

Build, installation, and release facts must be governed by real current project entries. If the project has no build system, installation artifact, binary release package, or resource generation process, write `not applicable`. Do not write one type of project script, preset, installation behavior, IDE configuration, generated directory, or platform toolchain as a default fact for all projects.

When only the six controlled documents, user documentation, or templated documents are modified and source code, public entries, API/interface boundaries, build scripts, test entries, or installation logic are not touched, build facts may be recorded as `not applicable` or `not executed`; build execution and reporting requirements belong to `AGENTS.md` and `agents/RULES.md`.

## 8. Test Entry Facts

| Test or verification category | Current entry | Coverage scope | Automation status | Notes |
| --- | --- | --- | --- | --- |
| `{{%TEST_OR_VERIFICATION_CATEGORY}}` | `{{%TEST_ENTRY}}` | `{{%TEST_COVERAGE_SCOPE}}` | `{{%AUTOMATION_STATUS}}` | `{{%NOTES}}` |

Test facts must distinguish automated tests, manual verification, interactive verification, performance observation, security verification, structural coverage, document quality, pre-release checks, and user acceptance. Performance prints, sample output, menu interaction, screenshots, logs, or temporary persisted results cannot replace correctness criteria unless the instantiated project explicitly defines them as verification entries and states their limitations.

When there is currently no entry for a type of test, write `not applicable` or `not established`. Only when that test entry is a verification capability the project should have but has not established should a follow-up plan be recorded in `agents/TODO.md` according to evidence. Do not write unestablished test entries as covered.

## 9. Current Capability Status

| Capability domain | Current status | Public entry | Evidence location | Test status | Notes |
| --- | --- | --- | --- | --- | --- |
| `{{%CAPABILITY_DOMAIN}}` | `{{%CURRENT_STATUS}}` | `{{%PUBLIC_ENTRY}}` | `{{%EVIDENCE_LOCATION}}` | `{{%TEST_STATUS}}` | `{{%NOTES}}` |

Capability status must be explicitly filled using statuses such as `released`, `preview`, `internal`, `placeholder`, `not implemented`, `deprecated`, and `not applicable`. Internal existence, skeletons, document mentions, reserved enum values, reserved configuration keys, or to-do plan records do not equal released capability.

When capability status changes, such as a placeholder module being completed, an internal capability being made public, a test entry being completed, release scope changing, a user manual chapter being added, or a to-do plan item being removed, this file, `agents/TODO.md`, and related controlled documents must be checked in sync.

## 10. Fact Maintenance Triggers

The following fact changes should trigger a synchronized check of this file:

- Changes to API, CLI, SDK, service, plugin, protocol, configuration, user interface, data format, model entry, deployment entry, operations entry, documentation entry, foundational types, public structures, export macros, calling conventions, or other public commitments.
- Changes to build entries, build systems, release processes, installation artifacts, resource generation, script behavior, container images, deployment methods, or package management information.
- Changes to responsibilities of public directories, source directories, runtime entries, test entries, build entries, document directories, installation artifact directories, generated directories, cache directories, or tool configuration directories.
- Changes to test entries, automation status, verification methods, performance observation, security verification, structural coverage, document quality, or result persistence conventions.
- Changes to current capability status, such as completion of placeholder capabilities, public release of internal capabilities, completion of test entries, narrowing of release scope, or closure of known issues.
- Changes to responsibility relationships among the six controlled documents, version synchronization rules, automatic quality-domain chain, quality-domain orchestration rules, automatic quality-loop rules, formal user manual maintenance boundaries, table-of-contents evolution rules, source-reading constraints, or confidentiality boundaries.
- Changes to rule ownership for underlying fact derivation, blocker handling, plan-readiness gates, explicit-assumption recording, or complex ordinary-task acceptance tie-back.
- Changes to document synchronization boundaries after code-fact changes, especially the distinction between small-scope fact synchronization in `agents/BASE.md` and triggering formal user manual generation/rewrite.

## Appendix

### Instantiation Checklist

This checklist is a representative template-stage checklist. During instantiation or later template maintenance, this file's full text **must first be scanned** for every valid `{{%...}}` placeholder and a deduplicated set must be established. This checklist ***must not replace*** full-file scan results. The ellipsis form `{{%...}}` does not count as a fill item when it is used only as syntax explanation. After instantiation is complete, this entire chapter and `### Placeholder Checklist` ***must be deleted*** and must not remain in formal output.

When instantiating this file, check and fill only factual fields within `agents/BASE.md`:

- Version and date: `{{%DOCUMENT_VERSION}}`, `{{%UPDATED_DATE}}`, synchronized document version identifiers, and factual scope.
- Project identity and positioning: `{{%PROJECT_NAME}}`, project domain, project type, primary delivery form, primary language or runtime, primary user role, primary maintainer role, and release scope.
- Public entry and source root: primary public entry, authoritative public-entry fact source, source or content root, runtime entry, public entry category, entry location or identifier, stability level, user responsibility, project responsibility, and notes.
- Compatibility and current-status tables: applicability, current facts, verification entries, and change risks for API, ABI, data format, configuration format, and protocol or service contract; capability domain, current status, public entry, evidence location, test status, and notes.
- Directory responsibilities: directory path, directory responsibility, external stability, fact notes, and distinctions among public entries, internal implementation, test entries, build entries, generated directories, installation artifacts, third-party dependencies, document directories, and tool configuration directories.
- Build, installation, release, and resource facts: build system, build entry, build configuration matrix, installation or release entry, release package structure, resource or metadata, verification methods, and notes.
- Test and verification facts: test or verification category, test entry, test coverage scope, automation status, performance observation, global security domain, structural coverage domain, document quality domain, pre-release checks, and user acceptance fact states.
- Evidence, status, and risk fields: covered public entry, fact source confidence, fact source notes, change risk, evidence location, test status, current capability status, and maintenance trigger conditions.
- Status words: statuses such as `not applicable`, `not established`, `placeholder`, `internal`, `preview`, `released`, and `deprecated` must be filled according to current project facts and must retain verifiable basis.

### Placeholder Checklist

This checklist lists at most 10 representative or key placeholders or categories. The full handling scope is governed by full-file scan results for valid `{{%...}}` placeholders. When any placeholder is added, deleted, or renamed, handling rules **must be updated** according to scan results. The items below ***must not be maintained alone***.

- Metadata: `{{%PROJECT_NAME}}`, `{{%DOCUMENT_VERSION}}`, `{{%UPDATED_DATE}}`
- Factual-scope entries: `{{%PRIMARY_PUBLIC_ENTRY}}`, `{{%PUBLIC_ENTRY_AUTHORITY}}`, `{{%SOURCE_OR_CONTENT_ROOT}}`, `{{%RUNTIME_ENTRY}}`
- Project positioning: `{{%PROJECT_DOMAIN}}`, `{{%PROJECT_TYPE}}`, `{{%PRIMARY_DELIVERY_FORM}}`, `{{%PRIMARY_LANGUAGE_OR_RUNTIME}}`
- Roles and release scope: `{{%PRIMARY_USER_ROLE}}`, `{{%PRIMARY_MAINTAINER_ROLE}}`, `{{%RELEASE_SCOPE}}`
- Public entry table: `{{%PUBLIC_ENTRY_CATEGORY}}`, `{{%PUBLIC_ENTRY_LOCATION_OR_IDENTIFIER}}`, `{{%STABILITY_LEVEL}}`, `{{%USER_RESPONSIBILITY}}`, `{{%PROJECT_RESPONSIBILITY}}`
- Fact source table: `{{%PUBLIC_ENTRY_FACT_SOURCE_CATEGORY}}`, `{{%COVERED_PUBLIC_ENTRY}}`, `{{%FACT_SOURCE_CONFIDENCE}}`, `{{%FACT_SOURCE_NOTES}}`
- Compatibility table: placeholder categories for applicability, current fact, verification entry, and change risk of API, ABI, data format, configuration format, and protocol or service contract
- Directory responsibilities: `{{%DIRECTORY_PATH}}`, `{{%DIRECTORY_RESPONSIBILITY}}`, `{{%EXTERNAL_STABILITY}}`, `{{%FACT_NOTES}}`
- Build, installation, and resources: `{{%BUILD_SYSTEM}}`, `{{%BUILD_ENTRY}}`, `{{%BUILD_CONFIGURATION_MATRIX}}`, `{{%INSTALLATION_ARTIFACT}}`, `{{%INSTALL_OR_RELEASE_ENTRY}}`, `{{%RESOURCE_OR_METADATA}}`
- Tests, capabilities, and evidence: `{{%TEST_OR_VERIFICATION_CATEGORY}}`, `{{%TEST_ENTRY}}`, `{{%TEST_COVERAGE_SCOPE}}`, `{{%AUTOMATION_STATUS}}`, `{{%CAPABILITY_DOMAIN}}`, `{{%CURRENT_STATUS}}`, `{{%EVIDENCE_LOCATION}}`
