# {{%PROJECT_NAME}} Engineering Rules

## 1. Version Information

- Current version: `{{%DOCUMENT_VERSION}}`
- Updated: {{%UPDATED_DATE}}
- Synchronized documents: `README.md {{%DOCUMENT_VERSION}}`, `AGENTS.md {{%DOCUMENT_VERSION}}`, `agents/RULES.md {{%DOCUMENT_VERSION}}`, `agents/BASE.md {{%DOCUMENT_VERSION}}`, `agents/TODO.md {{%DOCUMENT_VERSION}}`, `doc/DOCUMENTATION.md {{%DOCUMENT_VERSION}}`

## 2. Document Role

`agents/RULES.md` is the engineering rulebook and style constraint document for {{%PROJECT_NAME}}. It is shared by developers and agents. It carries core engineering principles, public-entry and compatibility boundaries, layering responsibilities, resource and hot-path rules, naming and data conventions, platform and dependency rules, automatic quality guard rules, build and delivery rules, document maintenance rules, and formal user manual writing rules.

This document is not an agent-private prompt, does not record current facts, does not carry follow-up plans, and does not replace the formal user manual. Project entry is governed by `README.md`; the agent control entry is governed by `AGENTS.md`; current facts are governed by `agents/BASE.md`; follow-up plans are governed by `agents/TODO.md`; the formal user manual is governed by `doc/DOCUMENTATION.md`.

This document must retain its constraint strength. Readability, brevity, refactoring, or merging convenience must not be used to delete, weaken, or blur strong constraints about public entries, compatibility, subagent orchestration, blocking conditions, TODO boundaries, document maintenance, or formal user manuals.

## 3. Core Engineering Principles

- Think Before Changing: before modifying code, interfaces, configuration, documents, or templates, the goal, boundary, impact scope, acceptance method, and rollback method must be clear. If requirements, semantics, compatibility, layering ownership, or user intent are ambiguous, clarify first.
- Simplicity First: prefer direct, verifiable, maintainable solutions. Do not create extra abstractions for one-off needs, and do not add capabilities that the user did not request and that are not necessary.
- Surgical Changes: modify only the locations needed to complete the goal. Do not opportunistically optimize, reorder, format, or rename unrelated content.
- Evidence Based: factual judgments must have verifiable evidence. When evidence is missing, report uncertainty only; do not write guesses as facts, supported capabilities, or user commitments.
- Preserve Worktree: respect the existing worktree state. Do not revert, overwrite, or rewrite existing user or agent changes unless the user explicitly asks.
- Preserve Constraints: meanings such as `must`, `must not`, `only`, `forbidden`, and `stop and report` must not be weakened into suggestions, preferences, options, or broad principles.

## 4. Public Entries, API/ABI, and Compatibility Constraints

A public entry is any user-visible, user-obtainable, and user-verifiable API, CLI, SDK, service, plugin, protocol, configuration, user interface, data format, model entry, deployment entry, operations entry, or documentation entry. An API is a usage contract between users and code, system interfaces, or programmatic entries; it is one kind of public entry. An ABI is a binary contract between code units and is enabled only when exported symbols, calling conventions, type layouts, link artifacts, or binary compatibility commitments exist.

- Do not call every public entry an API, and do not conflate API with ABI.
- When the project has public entries, `agents/BASE.md` must record their locations, authoritative fact sources, public contracts, stability levels, inputs and outputs, error boundaries, limitations, and user-visible results. Non-applicable entries must be marked as not applicable or removed; do not invent capabilities.
- Before changing public entries, parameter semantics, data layouts, protocol fields, configuration keys, error codes, status codes, user-visible behavior, compatibility commitments, or delivery artifacts, compatibility impact, migration cost, document synchronization, and verification coverage must be checked.
- Internal implementation details must not become user commitments. The formal user manual must not redefine engineering facts.
- C/C++, SDK, binary ABI, functional API, numerical library, resource object, buffer, session object, and equivalent models are conditional extensions only. Public macros, public types, function families, operator overloads, templates, buffers, complex layouts, handle lifecycles, calling conventions, and type layouts must not be written as mandatory checks for every project.
- When the project has public headers where applicable, public schemas, protocol documents, configuration descriptions, exported symbols, calling conventions, public type layouts, serialization formats, plugin structures, database structures, or message structures, the corresponding API, ABI, protocol, or format compatibility boundary must be stated separately.
- Do not claim support for platforms, hardware backends, algorithmic capabilities, service capabilities, command capabilities, configuration capabilities, or public entries that are not implemented, published, or verified.

## 5. Layering and Change Discipline

The instantiated project must map directories, modules, services, scripts, documents, generated outputs, and delivery artifacts to its real structure. The following `{{%...}}` fields represent responsibility categories that must be filled; they do not mean every project must have source directories, runtime entries, test entries, third-party dependencies, or installation directories.

- `{{%PUBLIC_ENTRY_PATH_OR_ID}}` carries user-visible contracts and stable adaptation points; it does not carry unrelated internal implementation details.
- `{{%FOUNDATION_LAYER_PATH_OR_ID}}` provides reusable foundation capabilities and must not depend on high-level business flows, demo entries, or release flows.
- `{{%CORE_IMPLEMENTATION_LAYER_PATH_OR_ID}}` carries core capabilities, state objects, service logic, data processing, or primary business flows.
- `{{%DOMAIN_EXTENSION_LAYER_PATH_OR_ID}}` carries domain extensions, plugins, models, specialized algorithms, or feature packages. Placeholder or skeletal capabilities must be clearly marked in `agents/BASE.md` and `agents/TODO.md`.
- `{{%THIRD_PARTY_DEPENDENCY_PATH_OR_ID}}` carries third-party, derived, or independent dependencies; do not modify it without an explicit need.
- `{{%RUNTIME_TEST_DEMO_GENERATION_MAINTENANCE_ENTRY_PATH_OR_ID}}` is responsible for runtime, tests, demos, generation, maintenance, observation, or result output. Stable implementation layers must not depend backward on these entry layers.

Internal implementation should first reuse internal helpers, script modules, service modules, data modules, configuration modules, or non-public implementation paths in the same or lower layer. Unless an external compatibility boundary, public wrapper behavior, or established project convention requires it, internal reuse should not call public wrappers, CLI entries, service endpoints, or public handle interfaces.

## 6. Resources, State, and Hot Paths

This chapter is enabled only when the project has real-time loops, large-scale data processing, state objects, streaming processing, service hot paths, resource-sensitive paths, numerical hot zones, or other explicit hot paths. If no such model exists, mark it as not applicable, but do not invent performance commitments.

- Hot paths must not introduce unplanned or unverified dynamic resource allocation, synchronization blocking, file IO, console IO, network blocking, exception leakage, log noise, thread creation, process startup, remote calls, or heavy initialization.
- Resource preparation should happen during construction, initialization, deployment, startup, connection establishment, task planning, or the preparation phase defined by the instantiated project. Execution should reuse existing resources, buffers, connections, caches, workspaces, coefficients, plan objects, or equivalent prepared artifacts.
- Reset, cleanup, release, reconnect, rollback, close, destroy, and retry behavior must be clearly defined and covered by verification. By default, reset only resets state and should not implicitly release resources or change capacity unless the public contract explicitly says so.
- Ownership, lifecycle, concurrent access, aliasing, error recovery, and invalidation rules must be recorded in a way users can understand.
- Whether inputs and outputs may overlap, share storage, be borrowed, cross thread boundaries, or be retained after invalidation must be explicitly stated. Without evidence, do not assume in-place use, concurrent use, or retention across invalidation points is safe.
- Performance observation cannot replace correctness verification. When performance targets, data sizes, or measurement methods change, they must be recorded in sync.

## 7. Types, Naming, Data, and Configuration

- Naming must follow the existing project style. Before adding new rules, check current facts, neighboring modules, public entries, and existing documentation conventions.
- Grouped capabilities, public entries, command families, endpoint groups, configuration families, data-format families, or functional API families must keep naming, parameters, fields, error boundaries, lifecycle, and documentation consistent.
- Once data structures, file formats, protocol fields, configuration keys, state values, error codes, return objects, event names, or page entries are public, they must remain compatible or provide migration guidance.
- Values, units, time zones, encodings, ordering, case sensitivity, null values, defaults, boundaries, open/closed ranges, lengths, capacities, and pagination semantics must be explicit.
- Do not introduce multiple names, multiple placeholder sets, or multiple status expressions for the same concept.
- When templates, generics, plugins, extension points, script entries, or type sets are unclear, do not assume the support scope. Confirm supported types, instantiation matrix, export range, test range, or documentation range first.
- Approximate numeric, probabilistic, statistical, graphical, time, currency, sensor, or business-threshold comparisons must use applicable tolerance. Integers, quotas, pagination, timestamps, money, and version ranges must define overflow, rounding, saturation, truncation, and boundary strategies.

## 8. Platforms, Tools, Acceleration, and External Dependencies

- Dependencies must have a clear purpose, version range, license boundary, alternative, and verification method.
- Do not claim support for unverified platforms, runtimes, hardware, deployment models, browsers, operating systems, databases, cloud services, plugin systems, or third-party services.
- Optional acceleration, specialized backends, platform features, GPU, SIMD, FPGA, vectorization, caching, batching, or service extensions must have capability detection, fallback paths, and equivalence verification.
- Do not delete the baseline implementation, scalar implementation, interpreter path, generic service path, fallback path, or compatibility path and keep only a specialized backend, unless the project explicitly does not commit to a generic fallback and has synchronized the public boundary.
- Third-party code, generated artifacts, external services, and user-defined extensions must not break public compatibility boundaries.
- When dependencies, toolchains, delivery flows, runtime environments, acceleration backends, or platform support change, facts and boundaries in `agents/BASE.md`, `agents/TODO.md`, and `doc/DOCUMENTATION.md` must be checked in sync.

## 9. Automatic Quality Guard and Verification

During every iteration, the agent must silently run the automatic quality guard appropriate to the change risk. The user does not need to trigger it manually. The quality guard has lightweight and full levels: the lightweight guard covers change scope, incremental risk, security boundaries, project facts, and document quality; the full guard covers public-entry impact, security model, structural coverage, deep verification, and formal manual output. Later quality activities depend on earlier checks; if an earlier check is incomplete, failed, blocked, or waiting for user judgment, later activities must not proceed.

- Every quality stage must have an independent task brief, input scope, output artifact, subagent orchestration, report, acceptance step, and TODO-candidate boundary. Later-stage conclusions must not replace earlier-stage acceptance.
- When subagents are supported, the agent must not proactively downgrade. If concurrency is insufficient, tasks must queue. If platform or session hard limits are exhausted, the agent must stop for continuation and preserve task briefs, temporary artifact state, and remaining queues. Only when no subagent capability exists may the work be downgraded into file-based, staged, or scoped phases.
- `explore` may be used only for read-only checks, exploration, fact verification, inventory building, review, and summary. `general` is used for writing, revision, merge work, version synchronization, TODO records, and formal document changes. Mixed read/write tasks must be split into read-only `explore` tasks and write-capable `general` tasks.
- A parent agent, session agent, or coordinator must not privately cancel, terminate, replace, merge, or declare failure merely because a subagent takes time, outputs a long report, progresses slowly, waits in a queue, or handles complex work. An unfinished subagent may end only when the user explicitly cancels, a platform hard limit is reached, the subagent returns completion/failure/blockage, or continuing would create unacceptable risk.
- When code, security, compatibility, test, build, fact, or document issues are found, the agent must not directly and without authority modify source code, public entries, build scripts, test entries, installation logic, or delivery flows. Issues with evidence locations, impact scope, current exposure, first action, and verification suggestions must be recorded within the `agents/TODO.md` boundary.
- Changes to public entries, deliverables, build/release flows, test entries, directory responsibilities, security boundaries, or formal user manuals must escalate to the full guard according to risk. Small document wording, formatting, or version-metadata-only changes may use the lightweight guard, but must still complete text validation and factual-boundary checks.
- Quality-guard output must be reviewable, traceable, and actionable. Low-confidence findings must only be reported and must not be disguised as confirmed issues.

The quality guard covers at least the following responsibility domains. These domain names are not manual user entry points; the agent must automatically organize them according to each iteration's change risk. When domains in the same iteration depend on each other, the preceding domain must be accepted before the next domain starts; stages must not be skipped, merged, or backfilled from later conclusions.

| Responsibility domain | Input scope | Required artifacts | Non-responsibilities |
| --- | --- | --- | --- |
| Incremental change domain | Current tracked changes, related public entries, test gaps, and document synchronization scope | Change coverage summary, incremental semantic risk, interface or compatibility risk, verification suggestions, uncovered scope | Does not replace full-repo coverage, security model, formal manual output, or cross-project impact judgment |
| Incremental security domain | Dangerous calls, input boundaries, permission boundaries, data flow, and resource lifecycle doubts in current changes | Security risk list, evidence locations, impact scope, confidence, first action | Does not write low-confidence items as confirmed issues and does not replace full-repo security modeling |
| Factual boundary domain | Six controlled document roles, public-entry facts, build/test entries, capability status, and version synchronization | Fact-difference list, documents needing synchronization, TODO candidates, residual risk | Does not directly rewrite formal manual content and does not replace document quality revision or full coverage |
| Document quality domain | Markdown, version numbers, metadata, wording, concept consistency, numeric units, TOC links, and writing quality | Fix summary, unresolved issues, format validation results, anti-weakening check results | Does not judge code facts and does not refresh public capability descriptions |
| Public impact domain | Public entries, API usage contracts, ABI or equivalent compatibility boundaries, downstream calls, delivery artifacts, and version strategy | Impact judgment, compatibility conclusion, migration or documentation synchronization suggestions, residual risk | Does not replace the security model or per-work-unit coverage |
| Global security domain | Assets, entries, trust boundaries, dependency boundaries, permissions, data, network, scripts, supply chain, and configuration surface | Threat model summary, risk matrix, evidence, confidence, TODO candidates | Does not fix code and does not write false positives as confirmed issues |
| Structural coverage domain | Owned files, parsable work units, script entries, configuration entries, data flows, routes, tasks, and generation entries | File coverage matrix, work-unit coverage matrix, uncovered items, confirmed findings, remaining queue | Does not replace security specialty checks, compatibility decisions, or manual output |
| Manual output domain | Public-entry matrix, stable facts, section briefs, drafts, merge work, review, and six-document alignment scope | Formal manual draft or revision, section acceptance, six-document alignment result, release review, residual risk | Does not replace the main responsibility of preceding quality domains and must not expose internal orchestration to the formal user manual |

Every responsibility-domain report must include at least: input scope used, capability detection result, preceding-domain acceptance state, subagent assignment, uncovered items, findings list, TODO write status, reasons for not writing items, verification results, and residual risk. Responsibility domains may reuse only read-only inventories and accepted fact sources; they must not reuse conclusions to replace their own checks.

## 10. Build, Delivery, and Text Validation

- If the project has build, deployment, packaging, release, generation, or installation flows, the default entry, required environment, artifact location, version strategy, and verification method must be recorded.
- When public entries, deliverables, configuration, directory responsibilities, verification entries, release flows, or runtime environments change, controlled documents must be updated in sync.
- If only documents are modified and implementation, public entries, delivery flows, and verification entries are untouched, a full build or release validation may be skipped, but the reason must be stated.
- After modifying any text file, encoding, line endings, trailing whitespace, EOF newline, and basic diff quality must be checked, and trailing whitespace must be removed.
- Markdown files must run markdownlint or an equivalent check. `MD013` line length may be exempted according to project convention; other structural, link, table, fence, list, and whitespace issues must be fixed.
- Text line endings, encoding, and EOF newline use `{{%TEXT_LINE_ENDING_POLICY}}`, `{{%TEXT_ENCODING_POLICY}}`, and the file-final-newline policy by default. During template use, the repository state may be used as a reference; a formal project must record the policy in `agents/BASE.md`.
- `git diff --check` or an equivalent whitespace check must pass. If the tool cannot run, state the reason, substitute check, and residual risk.

## 11. Document Maintenance

- The six controlled documents must have clear responsibilities, synchronized versions, and consistent cross-references. When any controlled document changes, responsibility scope, cross-references, and version synchronization must be checked.
- Fact changes primarily update `agents/BASE.md`; plan changes primarily update `agents/TODO.md`; rule changes primarily update `agents/RULES.md`; agent entry changes primarily update `AGENTS.md`; project entry changes primarily update `README.md`; formal user-facing instruction changes primarily update `doc/DOCUMENTATION.md`.
- When any of the six controlled documents is modified, all six document versions must be incremented and kept identical. If the instantiated project has a different version strategy, it must be explicitly defined in `AGENTS.md` and `agents/BASE.md`.
- The formal user manual only describes released capabilities and public preview capabilities with an explicit status. It must not expose internal maintenance rules, subagent orchestration, temporary processes, development directories, test entries, build scripts, source paths, internal object names, source line numbers, implementation flows, or unpublished dependencies.
- After document changes, grammar, syntax, ambiguity, concept conflicts, numeric units, reference chains, TOC links, Markdown structure, and writing quality must be checked.
- Completed process narrative is not retained by default. Only stable facts, constraints, verification results, or residual risks that affect future judgment enter the baseline.
- `{{%...}}` marks a template field. After this template is instantiated for a real project, every placeholder must be replaced, removed, or explicitly marked as not applicable. Published documents must not retain unexplained placeholders.

## 12. Facts, Issues, and TODO Boundaries

- `agents/BASE.md` records only currently verifiable facts. It does not record wishes, plans, guesses, historical process, or unconfirmed issues.
- `agents/TODO.md` records only confirmed issues, gaps, capability plans, or verification tasks that require follow-up. Items without an evidence location, impact scope, current exposure, first action, and verification suggestion must not be written.
- A reserved template field, placeholder section, user manual heading, or code skeleton must not be used to infer that the project already has a capability or must add a corresponding TODO.
- Closing, merging, downgrading, or deleting a TODO requires verification evidence. Incomplete items must not be written as completed.
- Security, compatibility, build, test, delivery, documentation fact, and public-entry issues must be written to the correct document according to responsibility; facts, rules, and plans must not be mixed.
- When the same issue appears in multiple documents, keep one primary record and use cross-references for impact scope. Do not maintain conflicting duplicate versions.

## 13. Formal User Manual Writing Rules

- The formal user manual is written for final users, not internal maintainers. It must be organized around user tasks, public entries, capability boundaries, parameter semantics, resource lifecycles, error boundaries, examples, and limits.
- The manual must first trim its TOC and body according to the public-entry matrix. Non-applicable API, CLI, SDK, service, plugin, protocol, configuration, user interface, data format, model entry, deployment entry, operations entry, or documentation entry must have corresponding sections, examples, indexes, and troubleshooting items removed, or be explained only in the matrix as not applicable.
- The default TOC covers all real `##` and lower headings in the body, excluding the document H1 and the `## Table of Contents` section itself. If the instantiated project explicitly requires including H1, TOC generation and checking scripts must use the same rule.
- Every major capability should explain purpose, applicability, qualitative principles, usage flow, inputs and outputs, notes, error boundaries, and complete examples. Principle explanations only describe public semantics, input/output relations, and user selection criteria; they must not describe internal algorithm steps, internal data structures, optimization paths, or source facts.
- Examples must use only public entries and public facts. They must not expose internal implementation, maintenance flows, temporary drafts, test entries, build scripts, source paths, internal object names, hidden handle mechanisms, or unpublished capabilities.
- Unpublished, unverified, incomplete, internal-only, or placeholder capabilities must not be written as released capabilities and must not appear in examples, indexes, or troubleshooting.
- Every public entry written into the manual must be checked against the corresponding declaration, implementation, public help, configuration description, service contract, data format, or use point to ensure parameter units, field semantics, ownership, aliasing limits, lifecycle, state progression, return values, error boundaries, and limits are genuinely usable.
- API and ABI descriptions must remain separate. ABI-sensitive facts apply only when the project has binary compatibility commitments and must focus on exported symbols, calling conventions, type layouts, enum underlying types, function pointers, structure field order, and link boundaries.
- The manual must not contain identifiable vendor names, product names, positioning evidence, internal material sources, competing product references, or sourcing traces from external reference material. The project's own public product name, brand name, release name, and user-visible materials are retained according to true public facts.
- Published manuals must not retain `{{%...}}` placeholders, template notes, generation rationale, maintenance flows, rule-section references, or QA-checklist phrasing.
