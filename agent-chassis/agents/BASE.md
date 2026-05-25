# {{%PROJECT_NAME}} Development Baseline

## 1. Version Information

- Current version: `{{%DOCUMENT_VERSION}}`
- Updated: {{%UPDATED_DATE}}
- Synchronized documents: `README.md {{%DOCUMENT_VERSION}}`, `AGENTS.md {{%DOCUMENT_VERSION}}`, `agents/RULES.md {{%DOCUMENT_VERSION}}`, `agents/BASE.md {{%DOCUMENT_VERSION}}`, `agents/TODO.md {{%DOCUMENT_VERSION}}`, `doc/DOCUMENTATION.md {{%DOCUMENT_VERSION}}`
- Factual scope: `{{%PRIMARY_PUBLIC_ENTRY}}`, `{{%PUBLIC_ENTRY_AUTHORITY}}`, `{{%SOURCE_OR_CONTENT_ROOT}}`, `{{%RUNTIME_ENTRY}}`, `{{%BUILD_ENTRY}}`, `{{%TEST_ENTRY}}`, `{{%INSTALL_OR_RELEASE_ENTRY}}`, `README.md`, `AGENTS.md`, `agents/RULES.md`, `agents/TODO.md`, `doc/DOCUMENTATION.md`

## 2. Document Role

`agents/BASE.md` is the project factual baseline. It carries the current project positioning, delivery model, public entries, compatibility boundaries, directory responsibilities, build and installation facts, test-entry facts, and current capability status.

This file does not carry agent control rules, detailed engineering rules, automatic quality-guard details, user manual writing rules, the formal user manual, follow-up plans, or known issue records. The agent control entry is governed by `AGENTS.md`; detailed engineering rules and user manual writing rules are governed by `agents/RULES.md`; the project summary is governed by `README.md`; follow-up plans and known issues are governed by `agents/TODO.md`; the formal user manual is governed by `doc/DOCUMENTATION.md`.

When source code, public entries, APIs/interfaces, build scripts, test entries, installation logic, directory responsibilities, or current capability status change as facts, this file should be updated in sync and the other controlled documents must be checked according to the version synchronization rules in `AGENTS.md`. If a code fact directly affects descriptions of released capabilities in the formal user manual, directly related small-scope text in `doc/DOCUMENTATION.md` may be synchronized. If the formal user manual needs to be fully generated or heavily rewritten from new code facts, follow the automatic quality guard and user manual writing rules in `agents/RULES.md`.

This file records facts only and does not expand automatic quality-guard orchestration. The current controlled-rule fact is that `agents/RULES.md` carries build and installation rules, document maintenance, quality guard, subagent lifecycle discipline, `explore`/`general` subagent type assignment, text-format validation including line endings, encoding, EOF newline, trailing whitespace removal, and formal user manual writing rules. Confirmed TODOs, factual gaps, and known issues should be recorded in `agents/TODO.md` according to responsibility.

## 3. Project Positioning

{{%PROJECT_NAME}} is a {{%PROJECT_TYPE}} in the {{%PROJECT_DOMAIN}} domain, with {{%PRIMARY_DELIVERY_MODEL}} as its primary delivery model. The project may be a local library, server application, CLI tool, frontend application, SDK, plugin, model, data engineering project, documentation project, or another engineering form. Instantiation must use the real project facts and must not inherit non-applicable technology-stack assumptions.

Current positioning table:

| Item | Content |
| --- | --- |
| Project type | {{%PROJECT_TYPE}} |
| Project domain | {{%PROJECT_DOMAIN}} |
| Primary language or runtime | {{%PRIMARY_LANGUAGE_OR_RUNTIME}} |
| Primary delivery model | {{%PRIMARY_DELIVERY_MODEL}} |
| Primary user role | {{%PRIMARY_USER_ROLE}} |
| Primary maintainer role | {{%PRIMARY_MAINTAINER_ROLE}} |
| Release scope | {{%RELEASE_SCOPE}} |

A public entry is any user-visible, user-obtainable, and user-verifiable API, CLI, SDK, service, plugin, protocol, configuration, user interface, data format, model entry, deployment entry, operations entry, or documentation entry. When the project has an API, the API is a usage contract between users and code, system interfaces, or programmatic entries. When the project has ABI commitments, the ABI is a binary contract between code units. Projects without a binary compatibility model must mark ABI as not applicable and must not invent ABI facts.

## 4. Public Entry and Compatibility Facts

Public-entry facts are filled by the instantiated project. Nonexistent entries must be marked as not applicable. Entries without verifiable sources must be marked as not established. Reserved template fields must not be used to infer public capabilities.

| Public entry category | Entry location or identifier | Stability level | User responsibility | Project responsibility | Notes |
| --- | --- | --- | --- | --- | --- |
| {{%PUBLIC_ENTRY_CATEGORY}} | `{{%PUBLIC_ENTRY_LOCATION_OR_ID}}` | {{%STABILITY_LEVEL}} | {{%USER_RESPONSIBILITY}} | {{%PROJECT_RESPONSIBILITY}} | {{%NOTES}} |

Authoritative public-entry fact sources must be recorded separately. Sources may include public declaration files, OpenAPI or protocol schemas, CLI help, SDK package metadata, user documents, plugin manifests, configuration documentation, UI entries, data-format documentation, model entry documentation, deployment documentation, operations documentation, or equivalent public material.

| Fact source category | Location or identifier | Covered entries | Confidence | Notes |
| --- | --- | --- | --- | --- |
| {{%PUBLIC_ENTRY_FACT_SOURCE_CATEGORY}} | `{{%PUBLIC_ENTRY_AUTHORITY}}` | {{%COVERED_PUBLIC_ENTRY}} | {{%FACT_SOURCE_CONFIDENCE}} | {{%FACT_SOURCE_NOTES}} |

Compatibility boundaries are filled by the instantiated project.

| Compatibility category | Applicable | Current fact | Verification entry | Change risk |
| --- | --- | --- | --- | --- |
| API | {{%API_APPLICABLE}} | {{%API_CURRENT_FACT}} | {{%API_VERIFICATION_ENTRY}} | {{%API_CHANGE_RISK}} |
| ABI | {{%ABI_APPLICABLE}} | {{%ABI_CURRENT_FACT}} | {{%ABI_VERIFICATION_ENTRY}} | {{%ABI_CHANGE_RISK}} |
| Data format | {{%DATA_FORMAT_APPLICABLE}} | {{%DATA_FORMAT_CURRENT_FACT}} | {{%DATA_FORMAT_VERIFICATION_ENTRY}} | {{%DATA_FORMAT_CHANGE_RISK}} |
| Configuration format | {{%CONFIG_FORMAT_APPLICABLE}} | {{%CONFIG_FORMAT_CURRENT_FACT}} | {{%CONFIG_FORMAT_VERIFICATION_ENTRY}} | {{%CONFIG_FORMAT_CHANGE_RISK}} |
| Protocol or service contract | {{%PROTOCOL_APPLICABLE}} | {{%PROTOCOL_CURRENT_FACT}} | {{%PROTOCOL_VERIFICATION_ENTRY}} | {{%PROTOCOL_CHANGE_RISK}} |

If the project is a C/C++ local library, binary-compatibility-sensitive project, numerical hot-path project, DSP project, or project tied to a specific build system, the corresponding conditional extension facts and constraints in `agents/RULES.md` must be filled and enforced. These facts must not be automatically applied to projects that do not use the corresponding technology stack.

## 5. Directory Responsibility Facts

| Path | Current responsibility | External stability | Maintenance rule |
| --- | --- | --- | --- |
| `{{%DIRECTORY_PATH}}` | {{%DIRECTORY_RESPONSIBILITY}} | {{%EXTERNAL_STABILITY}} | {{%MAINTENANCE_RULE}} |

Directory responsibilities must distinguish public entries, internal implementation, test entries, build entries, generated directories, installation artifacts, third-party dependencies, document directories, and tool configuration directories. Non-public directories must not be written into the user manual as stable usage entries. Generated directories, cache directories, and temporary directories must not be treated as factual authorities.

If the project has third-party, derived, or independent dependencies, the table should mark their boundaries, licenses or sources, whether modification is allowed, whether they are covered at the interface level, and whether they participate in release artifacts. If a corresponding directory does not exist, write not applicable; do not keep empty generic paths.

## 6. Build and Installation Facts

| Build or release item | Current fact | Entry location | Verification method | Notes |
| --- | --- | --- | --- | --- |
| Build system | {{%BUILD_SYSTEM}} | `{{%BUILD_ENTRY}}` | {{%BUILD_VERIFICATION_METHOD}} | {{%NOTES}} |
| Build configuration | {{%BUILD_CONFIGURATION_MATRIX}} | `{{%BUILD_CONFIGURATION_ENTRY}}` | {{%BUILD_CONFIGURATION_VERIFICATION_METHOD}} | {{%NOTES}} |
| Installation artifact | {{%INSTALLATION_ARTIFACT}} | `{{%INSTALL_OR_RELEASE_ENTRY}}` | {{%INSTALLATION_VERIFICATION_METHOD}} | {{%NOTES}} |
| Release package structure | {{%RELEASE_PACKAGE_STRUCTURE}} | `{{%RELEASE_PACKAGE_ENTRY}}` | {{%RELEASE_PACKAGE_VERIFICATION_METHOD}} | {{%NOTES}} |
| Resource or metadata | {{%RESOURCE_OR_METADATA}} | `{{%RESOURCE_GENERATION_ENTRY}}` | {{%RESOURCE_VERIFICATION_METHOD}} | {{%NOTES}} |

Build, installation, and release facts must be based on real current project entries. If the project has no build system, installation artifact, binary release package, or resource generation process, mark it as not applicable. Do not write scripts, presets, installation behavior, IDE configuration, generated directories, or platform toolchains from one project type as defaults for every project.

When only the six controlled documents, user documents, or template documents are modified and source code, public entries, APIs/interfaces, build scripts, test entries, and installation logic are untouched, a full build may be skipped. The final report must state why no build was run.

## 7. Test Entry Facts

| Test or verification category | Current entry | Coverage scope | Automation status | Notes |
| --- | --- | --- | --- | --- |
| {{%TEST_OR_VERIFICATION_CATEGORY}} | `{{%TEST_ENTRY}}` | {{%TEST_COVERAGE_SCOPE}} | {{%AUTOMATION_STATUS}} | {{%NOTES}} |

Test facts must distinguish automated tests, manual verification, interactive verification, performance observation, security-boundary checks, static checks, document quality checks, pre-release checks, and user acceptance. Performance prints, example output, menu interaction, screenshots, logs, or temporary output files cannot replace correctness criteria unless the instantiated project explicitly defines them as verification entries and states their limits.

When a test-entry class does not currently exist, write not applicable or not established. Only when the entry is a verification capability the project should have but has not yet established should a follow-up plan be recorded in `agents/TODO.md` with evidence. Do not write an unestablished test entry as covered.

## 8. Current Capability Status

| Capability domain | Current status | Public entry | Evidence location | Test status | Notes |
| --- | --- | --- | --- | --- | --- |
| {{%CAPABILITY_DOMAIN}} | {{%CURRENT_STATUS}} | `{{%PUBLIC_ENTRY}}` | `{{%EVIDENCE_LOCATION}}` | {{%TEST_STATUS}} | {{%NOTES}} |

Capability status must be explicitly filled as released, preview, internal, placeholder, not implemented, deprecated, not applicable, or an equivalent project-defined status. Internal existence, skeletons, document mentions, reserved enum values, reserved configuration keys, or TODO records do not equal released capability.

When capability status changes, for example when a placeholder capability is completed, an internal capability becomes public, a test entry is filled, release scope changes, a user manual section is added, or a TODO item is removed, this file, `agents/TODO.md`, and related controlled documents must be checked in sync.

## 9. Fact Maintenance Triggers

The following fact changes should trigger a synchronized check of this file:

- API, CLI, SDK, service, plugin, protocol, configuration, user interface, data format, model entry, deployment entry, operations entry, documentation entry, or other public commitment changes.
- Foundation types, public structures, export macros, calling conventions, public headers where applicable, public schemas, protocol documents, configuration descriptions, or equivalent public-entry changes.
- Build entries, build systems, release flows, installation artifacts, resource generation, script behavior, container images, deployment methods, or package-manager information changes.
- Responsibility changes for public directories, source directories, runtime entries, test entries, build entries, document directories, installation artifact directories, generated directories, cache directories, or tool configuration directories.
- Test entries, automation status, verification methods, performance observation, static checks, security-boundary checks, document quality checks, or result output conventions change.
- Current capability status changes, for example placeholder capability completion, internal capability publication, test entry completion, release scope reduction, or known issue closure.
- Responsibility relationships among the six controlled documents, version synchronization rules, automatic quality guard, subagent lifecycle discipline, `explore`/`general` subagent type assignment, formal user manual release scope, TOC evolution rules, source-reading constraints, user manual confidentiality boundaries, or full manual generation flow changes.

## 10. Placeholder Checklist

- `{{%PROJECT_NAME}}`
- `{{%DOCUMENT_VERSION}}`
- `{{%UPDATED_DATE}}`
- `{{%PROJECT_TYPE}}`
- `{{%PRIMARY_DELIVERY_MODEL}}`
- `{{%PRIMARY_PUBLIC_ENTRY}}`
- `{{%PUBLIC_ENTRY_AUTHORITY}}`
- `{{%BUILD_ENTRY}}`
- `{{%TEST_ENTRY}}`
- `{{%INSTALL_OR_RELEASE_ENTRY}}`
- `{{%CAPABILITY_DOMAIN}}`
