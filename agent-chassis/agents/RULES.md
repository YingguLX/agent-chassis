# `{{%PROJECT_NAME}}` Engineering Rules

## 1. Version Information

- Current version: `{{%DOCUMENT_VERSION}}`
- Updated date: `{{%UPDATED_DATE}}`
- Aligned documents: `README.md {{%DOCUMENT_VERSION}}`, `AGENTS.md {{%DOCUMENT_VERSION}}`, `agents/RULES.md {{%DOCUMENT_VERSION}}`, `agents/BASE.md {{%DOCUMENT_VERSION}}`, `agents/TODO.md {{%DOCUMENT_VERSION}}`, `doc/DOCUMENTATION.md {{%DOCUMENT_VERSION}}`

## 2. Document Role

`agents/RULES.md` is the detailed engineering rules and coding-style constraint document for `{{%PROJECT_NAME}}`, jointly followed by developers and agents. This document carries public entry and compatibility boundaries, layering, coding style, performance hot paths, conditional technology-stack extensions, tests, build, installation, build rules, plan management details, task plan gates, underlying fact derivation protocol, task risk level, automatic quality-loop rules, task orchestration rules, incremental difference domain, public impact domain, incremental security domain, global security domain, factual boundary domain, static analysis domain, document quality domain, documentation release domain, and formal user manual writing rules.

This document is not a private agent prompt, nor is it the current factual baseline or a future plan. Agent control entry rules are governed by `AGENTS.md`; current facts are governed by `agents/BASE.md`; the project overview is governed by `README.md`; future plans are governed by `agents/TODO.md`; the formal user manual is governed by `doc/DOCUMENTATION.md`.

## 3. Core Engineering Principles

### 3.1 Scope And Intent

- **Think Before Coding**: Before writing code, adjusting interfaces, or changing documentation, requirements, constraints, impact scope, and verification method must be understood first. When requirements, semantics, performance targets, compatibility, layer ownership, or user intent are ambiguous, the ambiguity must be made explicit and, when necessary, clarified with the user.
- **Challenge Assumptions**: Distinguish what must be true from what has merely always been done; facts, assumptions, goals, constraints, preferences, and risks must be distinguished first. When the existing approach conflicts with the underlying goal, prefer a more suitable approach based on underlying facts. Key assumptions that have not been verified must not be written as facts into code, documents, the to-do plan, or acceptance conclusions.
- **Intent Boundary**: Without an explicit user plan or instruction, large refactoring, adding / upgrading / removing dependencies, unrelated interface-signature or public-contract changes, module-structure migration, bulk renaming, or other high-impact actions beyond the current task boundary must not be planned or implemented by default. When truly necessary, the necessity, impact scope, smallest alternative, verification method, and rollback method must be stated first, and explicit user confirmation must be obtained.
- **Autonomous Within Boundaries**: When the current boundary is clear and risk is controllable, verifiable local low-risk work should proceed directly. When the goal is unclear, scope is unclear, key assumptions are unverified, a change is irreversible, sensitive information is involved, external resources are involved, a high-risk operation is involved, permissions conflict, or project constraints conflict, clarification must be concentrated, confirmation must be requested, or execution must stop and report. Non-blocking questions must not replace executable work.
- **Respect Boundaries**: Old issues that are found can be reported and suggested, but unrelated old code must not be deleted, changed, or refactored without authorization.
- **Simplicity First**: Prefer the smallest, most direct, verifiable solution. Features not explicitly requested by the user and not necessary must not be added, and one-off code must not receive broad abstraction.

### 3.2 Evidence And Indexing

- **Use Code Index When Available**: When the current workspace has available code indexes, symbol navigation, reference lookup, call relationships, code search, or semantic retrieval capability, code indexes should be used first to establish the initial factual scope. If indexes are unavailable, stale, insufficient in coverage, or conflict with source-reading results, degrade to source reading, file search, content search, and necessary verification. Code index results are only locating and coverage aids and ***must not replace*** current source code, public entries, or controlled-document facts.

### 3.3 Interfaces And Encapsulation

- **Stable Interfaces**: Prefer tightening immutability, readonly parameters, aliasing, lifecycle, and concurrency semantics inside implementations. Do not introduce new dependencies, and do not change unrelated public entries, API/ABI, function signatures, configuration formats, data structures, external behavior, build/test entries, or user-visible promises. If a change is necessary, state the underlying reason, impact scope, migration method, and rollback method.
- **Public Surface Encapsulation**: When writing or modifying public APIs, public headers where applicable, SDKs, exported symbols, public types, configuration contracts, protocol boundaries, or user-visible documents, information hiding and encapsulation boundaries must be preserved. Internal implementation signatures, private types, internal symbols, temporary helpers, internal file paths, state structures, caches, locks, schedulers, storage layouts, error stacks, debug entries, experimental switches, or other changeable implementation details must not be exposed or promised. Information exposed across the boundary must have a clear long-term compatibility reason, caller necessity, migration strategy, and verification method.
- **Minimal Scope and Namespace Hygiene**: New symbols, custom types, traits, helper procedures, temporary algorithm steps, module members, or exported objects should be placed in the smallest visibility scope that satisfies the current use. One-off local abstractions serving only a single function, code block, component, internal module flow, or algorithm step should prefer the language's natural local mechanisms, such as local types, local aliases, local functions, closures, lambdas, conditional dispatch, private internal types, or module-private definitions. They should be promoted to a wider scope only when reuse, a stable internal interface, cross-module collaboration, explicit specialization, or language limitations make that necessary. For public APIs, headers, SDKs, public types, exported symbols, configuration formats, or external contracts, expose only the minimum stable contract callers need to complete the task, based on clear long-term need, compatibility reason, and verifiable benefit; do not expose one-off implementation details or changeable internal structures.
- **No Anonymous Namespace By Default**: Unless the user explicitly requests it, generated or modified code must not use unnamed namespaces, anonymous namespaces, anonymous modules, anonymous global wrappers, or equivalent unnamed symbol-ownership mechanisms. Symbols, functions, methods, variables, custom types, helpers, and module members must have clear ownership, preferably in the smallest visible class, structure, module, named namespace, named file-private scope, or language-equivalent scope. If global namespace placement is truly necessary, it must be an explicit ownership choice and must not use an anonymous namespace to blur ownership, linkage boundaries, or maintenance responsibility.

### 3.4 Code Generation Defaults

- **Generate Compliant Code By Default**: New or rewritten code should be compliant with this chapter's engineering principles by default rather than repaired afterward. Code should default to immutability first, minimal mutability, shared readonly access, unique mutable access, explicit no-alias / readonly semantics, clear ownership, contained side effects, stable interfaces, and verifiable changes.
- **Explicit Data Flow and Side Effects**: Functions, modules, and interfaces should clearly distinguish readonly inputs, unique outputs, state with explicit lifetime, and configuration frozen after initialization. IO, logging, network, database, time, random numbers, caches, locks, scheduling, remote calls, and equivalent side effects should be explicit and kept at boundary layers so that hot paths do not hide side effects.
- **No Exceptions By Default**: Unless the user explicitly requests it, generated or modified code must not proactively introduce exception mechanisms, including `throw`, `raise`, `try`, `catch`, or `except`, and must not use exceptions as control flow, error propagation, input validation, or public contracts. Invalid input should be rejected at the earliest identified or captured boundary through the project's assertion mechanism, preconditions, type constraints, contract checks, or existing non-exception error channel, and must not be delayed into deep implementation. Exceptions inevitably thrown by external libraries, frameworks, or language runtimes may only be contained at boundaries and converted to the project's existing error expression, unless the user explicitly requests preserving exception semantics.

### 3.5 Data Ownership And Aliasing

- **Immutable By Default**: When language and scenario allow, variables, references, objects, collections, configuration, and resource handles should be immutable or readonly when no mutation is needed. Values, references, pointers, and pointed-to data with readonly access semantics should be declared immutable at the precise semantic level, clearly distinguishing immutable values, immutable references or pointers, immutable pointed-to data, and their combinations. In languages with a `const` system or equivalent semantics, distinguish `const T`, `const T *`, `T * const`, `const T * const`, or corresponding mechanisms to prevent accidental mutation and provide more information to compilers, IDEs, static analysis, and necessary constant propagation. When mutability is required, limit it to the smallest scope and do not promote temporary state to fields, globals, or shared context.
- **Single Writer and Clear Ownership**: When language and scenario allow, the same logical data should follow shared-readonly and unique-mutable principles in the same scope: multiple explicit readonly references may coexist, but data requiring write access must be expressed through a unique mutable entry. Function, method, and interface signatures should express ownership and read/write permissions where possible, so callers can tell from signatures who creates, consumes, reads, and exclusively writes. Resources must clearly identify creator, user, modifier, releaser, and sharing, caching, cross-thread, and async holding semantics.
- **Borrow-Checker-Like Code Generation**: Generated or modified code should default to signatures and implementations that express shared readonly access and unique mutable access: readonly inputs are explicitly immutable, writable outputs, mutable buffers, or state-advancement entries are exclusive, and scenarios that are both no-alias and readonly express both readonly and no-alias constraints. This is a language-neutral engineering constraint and must not be written as a Rust-only fact or used to override public contracts, caller compatibility, or test evidence for optimization.
- **Alias and Overlap Contracts**: When language and scenario allow, logically non-aliased memory access must be identified and expressed through `restrict`, unique mutable borrowing, readonly references, type wrappers, alias-restriction macros, or contract comments. Scenarios that are both no-alias and readonly should combine no-alias and readonly constraints. `restrict` or equivalent no-alias declarations can only be used when non-overlap has been proven, the public contract allows it, callers remain compatible, and tests cover the boundary; they ***must not*** be added by default for optimization. Dangerous areas with unproven overlap must not rely on implicit aliasing assumptions.
- **Semantics Before Optimization**: Immutability, single writer entries, pure functions, and side-effect isolation serve correctness and maintainability first. Do not treat these tightenings as performance silver bullets; performance-sensitive paths must be validated by measurement.

### 3.6 Change Discipline

- **Surgical Changes**: Modify only the locations required by the current request. Do not opportunistically optimize adjacent code, and do not change unrelated comments, formatting, structure, or names.
- **Minimal Invasiveness**: For modification tasks, unless the user explicitly requests broad refactoring, preserve existing naming rules, comment style, module structure, layering boundaries, and file organization; modify only the minimum scope required by the request.

### 3.7 Worktree And Constraint Protection

- ***Preserve Worktree***: When modifying any code or document, the existing worktree state must be respected. Other people's or users' existing changes must not be reverted unless the user explicitly requests it. Without explicit authorization in the current task, `git commit`, `git push`, `git tag`, `git release`, `git rebase`, `git reset`, `git checkout`, `git restore`, forced cleanup, or any other destructive Git operation must not be executed.
- ***Preserve Unrelated Changes***: If unrelated changes are found, do not revert or overwrite them. If unrelated changes do not affect the current task baseline or difference attribution, preserve them and continue the current task.
- ***Preserve Constraints***: Strong constraints such as "must", "must not", "can only", and "stop and report" must not be weakened to fit a template, reduce length, or improve readability.
- ***Protect Constraint Documents***: When maintaining `AGENTS.md`, project rules, command and agent configuration, verification gates, anti-weakening rules, or other documents carrying agent constraints, do not weaken, bypass, or delete protected constraints under the name of ordinary document maintenance, Markdown/format repair, or version synchronization unless the current task explicitly authorizes it.
- **Markdown File Format**: After a Markdown (`.md`) file is created or changed, it must be checked before persistence to ensure UTF-8 BOM encoding, CRLF line endings, no bare LF, preservation of the EOF newline, and no trailing whitespace; all Markdown format issues except `MD013` long-paragraph warnings must be repaired. If `markdownlint`, `npx markdownlint-cli`, or `npx markdownlint-cli2` is available in the current environment, it must be invoked to check Markdown (`.md`) files; if none is available, equivalent text checks must be performed, covering at least encoding, line endings, EOF newline, trailing whitespace, and statically identifiable Markdown format issues other than `MD013`.
- ***Preserve Text Format***: For all other text files, including non-binary text code files in every format, changes must preserve the original text encoding and line-ending format, preserve the EOF newline, and introduce no trailing whitespace. New other text files must use UTF-8 BOM encoding, CRLF line endings, no bare LF, preserve the EOF newline, and contain no trailing whitespace. Before executing a code or document modification task, the baseline of the target text file's encoding, line endings, EOF newline, and trailing whitespace must first be read; after writing, the persisted file must be rechecked. CRLF, LF, or other line-ending formats must not be mixed in the same file.

### 3.8 Recovery

- **Reversible Changes**: Changes must be explainable, verifiable, and reversible. If the rollback boundary, verification method, or impact scope cannot be explained, the approach must first be narrowed or execution must stop and report.
- **Failure Recovery**: After a failure, the failure cause must first be analyzed, the approach adjusted, and work continued within the current authorized scope. When a stop condition is triggered, verification information is insufficient, or continuing would expand risk, execution ***must stop and report*** completed scope, incomplete scope, recovery entry, and next-step recommendation.

## 4. Public Entries, API/ABI, and Compatibility Constraints

- Public entries are user-visible, obtainable, and verifiable APIs, CLIs, SDKs, services, plugins, protocols, configurations, user interfaces, data formats, model entries, deployment entries, operations entries, and documentation entries. An API is a usage contract between users and code, system interfaces, or programmatic entries, and is one or more public entries. An ABI is a binary contract between code and code, describing exported symbols, calling conventions, type layout, link artifacts, and binary compatibility boundaries. No document, review, or change description may fold all public entries into API, and API and ABI must not be mixed.
- This section is a conditional extension for public entries and compatibility. When a project has APIs, CLIs, SDKs, services, plugins, protocols, configurations, user interfaces, data formats, model entries, deployment entries, operations entries, or documentation entries, the corresponding public entry, API, or usage-contract facts must be filled in. When a project has exported symbols, calling conventions, public type layouts, link artifacts, or binary compatibility promises, ABI facts must be filled in. When the corresponding model does not exist, "not applicable" must be marked; public headers where applicable, binary ABI, functional API families, commands, services, or binary promises must not be fabricated.
- General public entry checks cover the genuinely applicable entry locations, user entry methods, public contracts, stability levels, inputs and outputs, error boundaries, limits, and user-visible results among APIs, CLIs, SDKs, services, plugins, protocols, configurations, user interfaces, data formats, model entries, deployment entries, operations entries, and documentation entries.
- Conditional extension checks are enabled only when the project has C/C++, an SDK, binary ABI, functional APIs, a numeric library, resource objects, buffers, session objects, or an equivalent model. Public macros, public types, function families, operator overloads, templates, buffers, complex structures, handle lifecycles, calling conventions, and type layouts must not be written as default required checks for all projects.
- `{{%PRIMARY_PUBLIC_ENTRY}}` is the authoritative collection of public entries or public usage contracts, and `{{%PUBLIC_ENTRY_AUTHORITY}}` is the fact source used to confirm those entries. When an entry also contains ABI-sensitive facts, exported symbols, calling conventions, type layouts, link artifacts, and compatibility boundaries must be described separately. Public headers where applicable, service documentation, CLI help, SDK types, configuration items, or data formats themselves must not be simply called ABI entries.

- Public entries, APIs, commands, endpoints, configurations, data formats, user interface entries, or usage contracts defined in `{{%PRIMARY_PUBLIC_ENTRY}}` must not be renamed, deleted, or reordered casually.
- When the project has a C/C++ native library, public headers where applicable, SDK headers, import/export macros, calling convention macros, aliasing macros, assertion macros, IO/memory helper macros, header-local class templates, header-local static objects, or cross-translation-unit public semantics, the ODR, thread safety, initialization, overridability, and user-visible side effects of public definitions such as `{{%IMPORT_EXPORT_MACRO_NAME}}`, `{{%CALLING_CONVENTION_MACRO_NAME}}`, `{{%ALIAS_RESTRICTION_MACRO_NAME}}`, `{{%BASIC_ASSERTION_MACRO_NAME}}`, `{{%CONTEXT_ASSERTION_MACRO_NAME}}`, `{{%SAVE_HELPER_MACRO_NAME}}`, `{{%READ_HELPER_MACRO_NAME}}`, `{{%BUFFER_REALLOCATION_MACRO_NAME}}`, `{{%POD_REALLOCATION_MACRO_NAME}}`, `{{%INPUT_STREAM_MACRO_NAME}}`, `{{%OUTPUT_STREAM_MACRO_NAME}}`, and `{{%NEWLINE_STREAM_MACRO_NAME}}` must not be broken. When no such model exists, "not applicable" must be marked; public headers where applicable or a macro system must not be fabricated.
- When the project exposes `{{%PRIMARY_LANGUAGE}}` operators, overloaded functions, class templates, generic types, decorators, annotations, extension methods, or other language-level public semantics, they are public entries, APIs, or compatibility surfaces. They must not be deleted, renamed, re-signed, hidden, or moved into internal implementation on the grounds that they are "not `{{%BINARY_COMPATIBILITY_MODEL}}`".
- When the project uses `{{%PRIMARY_LANGUAGE}}` header-local static objects, global helper objects, a shared-state model, or runtime singletons, the constraints defined by `{{%HEADER_INLINE_STATIC_OBJECT_CONTROL_MACRO_NAME}}` for `{{%HEADER_INLINE_SAVE_HELPER_OBJECT_NAME}}`, `{{%HEADER_INLINE_READ_HELPER_OBJECT_NAME}}`, `{{%HEADER_INLINE_REALLOCATION_HELPER_OBJECT_NAME}}`, and their `{{%HEADER_INLINE_STATIC_STORAGE_TYPE}}`/`{{%HEADER_INLINE_LOCK_OBJECT_TYPE}}` must be written clearly. They must not be changed to ordinary external declarations, inline definitions, local statics, lazy singletons, process-global state, or deletion without authorization.
- When public entries have input/output aliasing, buffer overlap, borrowed references, lifecycles, mutable views, or zero-copy semantics, `{{%ALIAS_RESTRICTION_MACRO_NAME}}` or an equivalent aliasing constraint must not be added, removed, or changed casually. Any change must check implementation, API description, callers, and tests together, and must state whether in-place, partially overlapping, or completely non-overlapping buffers are allowed.
- When public-entry parameters, buffers, resource handles, collection views, or data views have readonly, writable, input/output, shared-readonly, unique-mutable, no-alias, or overlap-allowed semantics, those semantics must be expressed consistently in public contracts, implementation, tests, and the user manual. `restrict`, `{{%ALIAS_RESTRICTION_MACRO_NAME}}`, or equivalent no-alias declarations may only be used when callers have been proven not to pass overlapping objects, the public contract allows it, and tests cover overlap/non-overlap boundaries; they ***must not*** be added by default for optimization.
- When the project has ABI-sensitive public types, serialized structures, protocol frames, database structures, plugin structures, message structures, or binary layouts, packing, field order, field type, visible size, pointer ownership semantics, and ABI or protocol layout of structures such as `{{%PUBLIC_TYPE_OR_ENUM_NAME}}` must not be changed. When no binary or format compatibility promise exists, "not applicable" must be marked; layout promises must not be fabricated.
- When a public structure, object, or resource handle contains `void*`, `{{%PUBLIC_STRUCT_ASSOCIATED_POINTER_TYPE}}*`, raw pointers, borrowed references, handles, file descriptors, connection objects, or external resource identifiers, it must not be casually changed to caller-frees, project-frees, smart pointers, container objects, managed references, copy-return models, or implicit lifecycles. The corresponding implementation, callers, binding layers, and tests must be checked before modification.
- When the project exposes `{{%PRIMARY_LANGUAGE}}` enums, fixed value sets, status codes, error codes, protocol values, or configuration values, their underlying type, enum value order, names, numeric semantics, defaults, or unknown-value handling must not be changed without compatibility verification, and they must not be casually changed to macro constants, integer parameters, string values, or other expressions with different compatibility.
- When the project exposes callbacks, function pointers, event handlers, hooks, task closures, async notifications, or plugin entries, signatures, calling threads, calling conventions, exception boundaries, `noexcept`, `noexcept(true)`, `noexcept(false)`, `const`, exclusive semantics, references, user-data parameters, return types, or object lifecycle promises must not be changed.
- When the project has ABI complex types, vector types, matrix layouts, frame formats, binary records, network packets, or fixed-endian structures, public layout must not be replaced by language-library internal objects or implementation-related containers. Layout, element order, byte order, alignment, and units must preserve public compatibility promises.
- When the project exposes grouped interfaces, public entry groups, functional API families, command families, service endpoints, configuration families, resource lifecycles, or object lifecycles, the public entry matrix, API symbol matrix, or equivalent usage contract that has already been published must not be changed without permission, especially `{{%CREATE_ENTRY_VERB}}` / `{{%PROCESS_ENTRY_VERB}}` / `{{%RESET_ENTRY_VERB}}` / `{{%DESTROY_ENTRY_VERB}}` and related input, output, bind, capacity, access, count, size, load, open, generate, submit, query, or close entries.
- When a state object, resource object, or session object in the project already requires explicit `{{%STATE_OBJECT_CONFIGURATION_PARAMETER_NAME}}` and `{{%RESOURCE_OBJECT_CONFIGURATION_PARAMETER_NAME}}`, implicit defaults, old-compatible signatures, or new overloads must not be restored without aligning API/ABI or usage-contract design, public declarations, implementation definitions, installation artifacts, and caller verification.
- When the project has highly repetitive interface layers, C/C++ public headers where applicable, `{{%EXTERNAL_LINKAGE_MODEL}}` wrappers, exported symbols, or ABI-sensitive public entries, public declarations, public headers, Doxygen / documentation groups, exported symbols, calling conventions, parameter order, return types, `{{%ALIAS_RESTRICTION_MACRO_NAME}}` / `const`, and ABI-visible structures must remain explicit and verifiable. Generative macros must not define public APIs backward, must not complete unpublished type combinations, and must not hide public declarations.
- When the project has data parallelism, hardware acceleration, GPU, SIMD, FPGA, vectorization, or other optimized backends, scalar implementations, baseline implementations, interpreter paths, or fallback paths must not be deleted so that only `{{%COMPATIBLE_VECTOR_ACCELERATION_ISA}}`/`{{%BASE_VECTOR_ACCELERATION_ISA}}`/`{{%DEFAULT_VECTOR_ACCELERATION_ISA}}` and other `{{%DATA_PARALLEL_ACCELERATION_BACKEND}}` paths remain, unless the project explicitly does not promise a general fallback and the public boundary has been aligned.
- Support for platforms, hardware backends, or algorithmic capabilities that have not been implemented must not be claimed without permission.
- When the project is a C/C++ native library or another native binary-compatibility-sensitive project, the current public headers where applicable must not be casually "C-ified" or split into `{{%PURE_LANGUAGE_SUBSET_COMPATIBILITY_MODEL}}` headers. To support `{{%PURE_LANGUAGE_SUBSET_COMPATIBILITY_MODEL}}` consumers, a compatible entry must be designed separately and ABI, installation artifacts, and existing `{{%PRIMARY_LANGUAGE}}` callers must be verified. Non-native-library projects must mark this item as "not applicable" and must not fabricate public headers where applicable on this basis.

## 5. Layering and Change Discipline

This chapter is the general layering rule. An instantiated project must map directory responsibilities to its own real structure. The following `{{%...}}` paths or responsibility patterns only indicate responsibility categories that need to be filled in; they do not mean every project must have source code, runtime entries, test entries, third-party dependencies, or installation directories.

- `{{%PUBLIC_ENTRY_PATH_OR_IDENTIFIER}}` is the authoritative entry for public usage contracts. When an instantiated project has public headers where applicable, public schemas, protocol documents, configuration descriptions, exported symbols, calling conventions, base layouts, `{{%PRIMARY_LANGUAGE}}` public semantics, or ODR-sensitive surfaces, they must be explicitly marked under this item; if absent, write "not applicable".
- `{{%BASE_CAPABILITY_LAYER_PATH_OR_IDENTIFIER}}` provides the base capability layer and does not carry high-level business logic, domain algorithms, user interaction, or release processes.
- `{{%CORE_IMPLEMENTATION_LAYER_PATH_OR_IDENTIFIER}}` implements the core capabilities, conditional algorithms, state objects, service logic, data processing, or main business flows of `{{%PROJECT_DOMAIN_SHORT_NAME}}`. When expensive preparation and high-frequency execution paths exist, expensive work should be completed during preparation and existing resources reused during execution.
- `{{%DOMAIN_EXTENSION_LAYER_PATH_OR_IDENTIFIER}}` carries the instantiated project's domain extensions, business capabilities, plugins, models, special algorithms, or feature packages. If the current `{{%DOMAIN_EXTENSION_PLACEHOLDER_IMPLEMENTATION_FILE_PATTERN}}` is still a skeleton or placeholder implementation, factual details are in `agents/BASE.md`.
- `{{%THIRD_PARTY_DEPENDENCY_PATH_OR_IDENTIFIER}}` carries third-party, externally maintained, or independent dependency implementations. Do not modify it without a clear requirement.
- `{{%RUN_TEST_DEMO_GENERATE_MAINTENANCE_ENTRY_PATH_OR_IDENTIFIER}}` is responsible for runtime entries, test entries, demo entries, generation entries, maintenance entries, observability entries, or result persistence. Stable implementation layers must not depend backward on these entry layers. If the instantiated project uses specific constraints from source directories to runtime-entry directories, they must be filled in `agents/BASE.md`; no directory name may be written as a generic default fact.
- Internal implementation should prefer reuse through same-layer or lower-layer internal helpers, templates, classes, script modules, service modules, data modules, configuration modules, or non-public implementation paths. Unless ABI boundary semantics, outward wrapping behavior, or nearby module convention clearly requires it, public exported functions, `{{%EXTERNAL_LINKAGE_MODEL}}` wrappers, CLI entries, service endpoints, or public handle interfaces *should not be called for internal reuse*.

## 6. Hot Paths and State Management

This chapter is a conditional extension for performance hot paths. The itemized hot-path constraints in this chapter are enabled only when the project has real-time processing loops, large-scale data processing, state objects, streaming processing, resource-sensitive paths, numeric hot spots, high-frequency service paths, or other clear hot paths. Projects without a hot-path model must mark "not applicable", but must still not fabricate performance promises.

- General hot paths prohibit dynamic resource allocation, blocking coordination, file IO, console IO, network blocking, exception escape, logging printouts, thread creation, process startup, remote calls, or other behavior that would break latency, throughput, reentrancy, or resource limits unless it has been designed and verified.
- Hot paths include high-frequency processing entries, batch-processing main loops, streaming loops, high-frequency service request paths, queue-consumption loops, scheduler loops, rendering loops, data-conversion loops, vector-kernel loops, numeric-computation loops, or other resource-sensitive paths declared by the instantiated project. `Process_*`/`process()`, frequency-domain transforms, filter sample loops, resampling loops, and `{{%NUMERICALLY_CONTROLLED_OSCILLATOR_CAPABILITY_NAME}}` sequence-generation loops are only conditional examples for native-library, numeric, or DSP projects and must not be written as the default model for all projects.
- If a one-off helper, command, SDK method, page action, service endpoint, or batch task performs computation by constructing temporary objects, it must be treated as a non-hot-path interface; it must not be called in a loop or claimed to be allocation-free, blocking-free, or constant-latency.
- Resource preparation should be completed during construction, initialization, deployment, startup, connection establishment, task planning, or the preparation phase defined by the instantiated project. Processing only reuses existing resources, buffers, connections, caches, workspaces, coefficients, plan objects, or equivalent prepared artifacts.
- The default responsibility of `reset()`, reset commands, reset interfaces, or equivalent state rollback entries is to reset state. Unless an existing module already has a clear design and test coverage, do not change capacity, reallocate large memory blocks, or change externally observable resource semantics.
- Input/output buffer aliasing relationships must be explicitly described. If in-place operation is allowed, safety must be proven; otherwise naming, assertions, or `{{%ALIAS_RESTRICTION_MACRO_NAME}}` constraints must clearly prohibit it.
- `{{%IO_BASE_CAPABILITY_IDENTIFIER}}`, `{{%FILE_IO_CORE_PATH_PATTERN}}`, container lifecycle interfaces, task creation/destruction, parallel object creation/destruction, service start/stop, or deployment entries may perform IO, allocation, connection, or thread management within their clear responsibilities. These behaviors must not spread into `{{%PROJECT_DOMAIN_SHORT_NAME}}` processing loops, batch-processing main loops, or high-frequency service paths.
- Save helpers, standard output, menu interaction, page demos, log observability, diagnostic output, debug tracing, and demo data generation in `{{%TEST_OR_OBSERVABILITY_ENTRY_PATTERN}}` belong only to test, observability, or demo paths; they must not be copied into library hot paths, high-frequency service paths, production scheduling paths, or low-latency paths users can rely on.

## 7. Types, Naming, and Reuse

This chapter defines the type system, naming matrix, and reuse rules. If the project has no public type suffixes, exported wrappers, numeric types, template instantiations, or ABI exposure scope, the corresponding items must be marked "not applicable"; when the corresponding model exists, naming consistency, type support scope, and testing responsibility in this chapter must still be preserved.

- Prefer existing project types and naming style in nearby files. Do not introduce another set of casing, abbreviation, or suffix rules.
- When implementing scalar, complex, base mathematical operations, domain base operations, or public-entry helper capabilities, first check existing `{{%PRIMARY_LANGUAGE}}` operator overloads, global utility functions, service utilities, script helpers, or configuration helpers in `{{%PRIMARY_PUBLIC_ENTRY}}`, such as `{{%BASE_OR_DOMAIN_UTILITY_FUNCTION_NAME_1}}`, `{{%BASE_OR_DOMAIN_UTILITY_FUNCTION_NAME_2}}`, `{{%BASE_OR_DOMAIN_UTILITY_FUNCTION_NAME_3}}`, `{{%BASE_OR_DOMAIN_UTILITY_FUNCTION_NAME_4}}`, `{{%BASE_OR_DOMAIN_UTILITY_FUNCTION_NAME_5}}`, `{{%BASE_OR_DOMAIN_UTILITY_FUNCTION_NAME_6}}`, `{{%BASE_OR_DOMAIN_UTILITY_FUNCTION_NAME_7}}`, `{{%BASE_OR_DOMAIN_UTILITY_FUNCTION_NAME_8}}`, `{{%BASE_OR_DOMAIN_UTILITY_FUNCTION_NAME_9}}`, `{{%BASE_OR_DOMAIN_UTILITY_FUNCTION_NAME_10}}`, `{{%BASE_OR_DOMAIN_UTILITY_FUNCTION_NAME_11}}`, `{{%BASE_OR_DOMAIN_UTILITY_FUNCTION_NAME_12}}`, `{{%BASE_OR_DOMAIN_UTILITY_FUNCTION_NAME_13}}`, `{{%BASE_OR_DOMAIN_UTILITY_FUNCTION_NAME_14}}`, `{{%BASE_OR_DOMAIN_UTILITY_FUNCTION_NAME_15}}`, `{{%BASE_OR_DOMAIN_UTILITY_FUNCTION_NAME_16}}`, `{{%BASE_OR_DOMAIN_UTILITY_FUNCTION_NAME_17}}`, `{{%BASE_OR_DOMAIN_UTILITY_FUNCTION_NAME_18}}`, and `{{%BASE_OR_DOMAIN_UTILITY_FUNCTION_NAME_19}}`; reuse them when they can be reused.
- If a base mathematical capability has an error, repair the same-family base implementation centrally and add coverage; do not scatter bypasses or copied correction logic across calling modules.
- When adding or adjusting grouped public entries, entry groups, functional API families, command families, endpoint groups, configuration families, data-format families, or similar public entries, naming must preserve the existing matrix of "capability domain + action + type suffix/entry variant".
- When the project has a public function suffix or type suffix matrix, casing styles usually include `{{%FLOAT32_PUBLIC_TYPE_SUFFIX}}` / `{{%FLOAT64_PUBLIC_TYPE_SUFFIX}}` / `{{%COMPLEX_FLOAT32_PUBLIC_TYPE_SUFFIX}}` / `{{%COMPLEX_FLOAT64_PUBLIC_TYPE_SUFFIX}}` / `{{%SIGNED_FIXED8_PUBLIC_TYPE_SUFFIX}}` / `{{%COMPLEX_FIXED8_PUBLIC_TYPE_SUFFIX}}` / `{{%UNSIGNED_FIXED8_PUBLIC_TYPE_SUFFIX}}` / `{{%UNSIGNED_FIXED16_PUBLIC_TYPE_SUFFIX}}` / `{{%UNSIGNED_FIXED32_PUBLIC_TYPE_SUFFIX}}` / `{{%UNSIGNED_FIXED64_PUBLIC_TYPE_SUFFIX}}`; internal types and template names often use lowercase suffixes such as `{{%FLOAT32_INTERNAL_TYPE_SUFFIX}}` / `{{%COMPLEX_FLOAT32_INTERNAL_TYPE_SUFFIX}}` / `{{%UNSIGNED_FIXED8_INTERNAL_TYPE_SUFFIX}}`. If no such matrix exists, mark "not applicable".
- When adding or adjusting parameters, options, fields, or request names for grouped public entries, entry groups, functional API families, command families, endpoint groups, configuration families, or data-format families, follow the short-name conventions in the current declaration matrix, such as `{{%PUBLIC_PARAMETER_NAMING_CONVENTION_1}}`, `{{%PUBLIC_PARAMETER_NAMING_CONVENTION_2}}`, `{{%PUBLIC_PARAMETER_NAMING_CONVENTION_3}}`, `{{%PUBLIC_PARAMETER_NAMING_CONVENTION_4}}`, `{{%PUBLIC_PARAMETER_NAMING_CONVENTION_5}}`, and `{{%PUBLIC_PARAMETER_NAMING_CONVENTION_6}}`.
- When adding or adjusting outward entry groups, functional API families, or exported wrapper implementations, non-code projects should use the instantiated project's real command, endpoint, configuration, or data-format generation rules and must not fabricate exported functions. Projects without repeated C/C++ C linkage wrappers must mark "not applicable" and must not fabricate exported wrappers for template completeness. When highly repetitive C/C++ C linkage wrapper definitions exist, the public declaration layer must remain explicit, and repeated wrapper definitions in the `.cpp` implementation layer should be organized as `static inline helper + MATRIX X-MACRO + ACTION DEFINE MACRO`.
- C/C++ C linkage wrapper definition matrixization applies only to the repeated exported wrapper layer inside the current `.cpp` translation unit. Helpers, matrix macros, and action macros must be limited to the current `.cpp` file. Macro definitions must be outside the `extern "C"` block, and macro expansion that generates exported implementation functions must be inside the `extern "C"` block. Macros only generate the exported wrapper layer and must not hide algorithm bodies, state advancement logic, numeric hot paths, or resource ownership semantics.
- C/C++ C linkage wrapper matrixization must be organized in this order: `template static inline __xmacro_helper_accel_$#action$_t` function template -> `$#LIBNAME$_API_MATRIX(X)` X-Macro matrix -> `$#LIBNAME$_DEFINE_$#ACTION$` action macro -> execute `$#LIBNAME$_API_MATRIX($#LIBNAME$_DEFINE_$#ACTION$);` per action inside `extern "C"` -> `#undef $#LIBNAME$_API_MATRIX` and all `#undef $#LIBNAME$_DEFINE_$#ACTIONn$`. `$#LIBNAME$`, `$#ACTION$`, `$#ACTION0$`, `$#ACTION1$`, `$#ACTION2$`, and `$#action$` are only code-skeleton metvariables in this document for explaining naming-fragment substitution; they are not `{{%...}}` template placeholders, are not added to the template placeholder list, are not added to fixed protocol fields, and must not enter real C/C++ source code as literals.
- The type matrix for C/C++ C linkage wrappers uses the `$#LIBNAME$_API_MATRIX(X)` form. Matrix entries must explicitly list type suffix, handler type, internal implementation type, input/output type, scalar type, error label, special cast type, and other fields needed to generate wrappers. Action macros use the `$#LIBNAME$_DEFINE_$#ACTION$` form; `$#ACTION$` uses uppercase action names such as `CREATE`, `ENSURE`, `PROCESS`, `RESET`, `DESTROY`, and `SET_PARAMS`. Each public action must be split into an independent action macro; a single large macro must not generate the entire family of all actions at once.

C/C++ C linkage wrapper multi-action expansion must preserve the following generic skeleton semantics, and `__xmacro_helper_accel_$#action$_t` only represents an in-project wrapper code pattern and must not be promoted into a cross-project public-header naming requirement:

```cpp
#ifdef __cplusplus
extern "C" {
#endif
    $#LIBNAME$_API_MATRIX($#LIBNAME$_DEFINE_$#ACTION0$);
    $#LIBNAME$_API_MATRIX($#LIBNAME$_DEFINE_$#ACTION1$);
    $#LIBNAME$_API_MATRIX($#LIBNAME$_DEFINE_$#ACTION2$);
#ifdef __cplusplus
}
#endif

#undef $#LIBNAME$_API_MATRIX
#undef $#LIBNAME$_DEFINE_$#ACTION0$
#undef $#LIBNAME$_DEFINE_$#ACTION1$
#undef $#LIBNAME$_DEFINE_$#ACTION2$
```

- Generated C/C++ C linkage wrapper definitions must match public declarations item by item and must not change exported symbols, signatures, parameter order, calling conventions, error strings, assertion order, release order, handler lifecycle, `{{%ALIAS_RESTRICTION_MACRO_NAME}}` / `const` semantics, or algorithm behavior. No concrete project's public header path, module name, matrix macro name, or concrete function family may be written as a generic default fact.
- Existing type suffixes, command variants, endpoint variants, or configuration matrices are defined per module. Not every module supports the full set of floating-point, complex, fixed-point, unsigned, command-form, or request-form combinations. Before adding, filling, or deleting interfaces, compare against neighboring public entries to confirm the module's existing matrix; do not mechanically copy suffix sets across modules or fill seemingly missing types on your own.
- When the project has floating-point, probability, statistical, graphics, time, currency, sensor, or other approximate numeric results, comparisons must use applicable tolerance or business thresholds. Numeric/DSP projects must not compare results from `{{%FREQUENCY_DOMAIN_TRANSFORM_FUNCTION_FAMILY}}`, `{{%INVERSE_FREQUENCY_DOMAIN_TRANSFORM_FUNCTION_FAMILY}}`, `{{%VARIABLE_FREQUENCY_TRANSFORM_FUNCTION_FAMILY}}`, filtering, phase, or power for exact equality.
- Overflow, saturation, truncation, rounding, and closed-interval strategies for fixed point, integer boundaries, quotas, pagination, timestamps, currency, version ranges, or other discrete boundaries must follow existing public facts and implementation. Do not assume behavior without evidence.
- When implementing class templates, function templates, generic containers, type-erased wrappers, or any capability whose type set is unclear, do not assume the supported type set, instantiation matrix, or ABI exposure scope on your own. First confirm with the user which types need support and which type combinations need explicit instantiation, export, or tests.
- Outward handles, sessions, connections, tasks, resource objects, and vector objects remain opaque. Public headers where applicable, SDKs, service descriptions, or public entries expose only necessary declarations or resource identifiers; internal objects continue to be carried by `{{%INTERNAL_HANDLE_CARRIER_MECHANISM}}` or the wrapping method already used by nearby modules.

## 8. Acceleration Backends and Data-Parallel Conditional Extensions

This chapter is a conditional extension for acceleration backends, data parallelism, numeric hot paths, and frequency-domain utilities. The rules in this chapter are enabled only when the project has SIMD, GPU, vectorization, parallel acceleration, batch execution, frequency-domain transforms, signal processing, or other data-parallel backends. Projects without these backends must mark "not applicable" and must not claim support for unverified hardware, libraries, or algorithm paths merely for template completeness.

- `{{%DATA_PARALLEL_ACCELERATION_BACKEND}}` must be enabled under the instantiated project's real gating system. If the project has compile macros, runtime probes, configuration switches, environment variables, hardware capability detection, server-side feature flags, or package-level options, defaults, enable conditions, disable conditions, and user-visible boundaries must each be written clearly; if absent, mark "not applicable".
- When the project has `{{%FREQUENCY_DOMAIN_TRANSFORM_FUNCTION_FAMILY}}`, `{{%FREQUENCY_DOMAIN_DEPENDENCY_NAME}}`, or other independent acceleration dependencies, the main-project acceleration gate, dependency's own acceleration gate, scalar fallback, platform branch, and precision branch must each be written clearly. No `{{%VECTOR_ACCELERATION_COMPILE_GATE_MACRO}}`, build option, or dependency default behavior may be written as a unified control fact for all frequency-domain paths.
- Do not mistakenly assume that one public macro, configuration key, environment variable, build option, runtime probe, or dependency default behavior controls every `{{%FREQUENCY_DOMAIN_UTILITY_CATEGORY}}` `{{%DATA_PARALLEL_ACCELERATION_BACKEND}}`.
- When the project is a C/C++ numeric library, native library, or data-parallel-backend-sensitive project, rules for `{{%PRIMARY_PUBLIC_ENTRY}}`, `{{%ACCELERATION_CONFIGURATION_HEADER_FILE}}`, `{{%COMPILER_OR_TOOLCHAIN}}`, `{{%TARGET_ARCHITECTURE_32_BIT}}`, `{{%PLATFORM_ARCHITECTURE}}`, toolchain-specific import/export attributes or calling convention keywords such as `__declspec`/`__cdecl`, and intrinsics are conditional extensions for that technology stack only. Non-`{{%COMPILER_OR_TOOLCHAIN}}`, non-`{{%TARGET_ARCHITECTURE_32_BIT}}`, or cross-platform support must not be assumed by default.
- `{{%DATA_PARALLEL_ACCELERATION_BACKEND}}` paths must preserve verifiable scalar fallback and non-multiple tail handling.
- Unless the caller has explicitly provided a strong alignment guarantee, prefer load/store strategies that are safe for unaligned input.
- When modifying `{{%FREQUENCY_DOMAIN_TRANSFORM_FUNCTION_FAMILY_COLLECTION}}` paths, the alignment allocation, `work` buffer size, `reorder` semantics, forward/inverse scaling, and real/complex input/output mapping for `{{%SINGLE_PRECISION_FREQUENCY_DOMAIN_DEPENDENCY_NAME}}`/`{{%DOUBLE_PRECISION_FREQUENCY_DOMAIN_DEPENDENCY_NAME}}` must be verified together.
- Intrinsics loops must not be rewritten hastily before alignment, aliasing relationships, tail-length handling, and numeric equivalence have been verified.

## 9. Capability Expansion, Algorithm Conditional Extensions, and Tests

This chapter defines capability expansion, algorithm conditional extensions, and verification matrix rules. When the project has no algorithm or special capability modules, algorithm-related items must be marked "not applicable", but the general change discipline of "confirm ownership first, implement a verifiable version first, then expose public entries, then align tests and documentation" must still be preserved. C/C++, DSP, frequency-domain transforms, SIMD, CMake, and similar specialized content is enabled only when the instantiated project has the corresponding technology stack.

1. Confirm change ownership first: base capabilities go under `{{%BASE_CAPABILITY_LAYER_PATH_OR_IDENTIFIER}}`; general `{{%PROJECT_DOMAIN_SHORT_NAME}}` core capabilities, conditional algorithms, state objects, core services, or main business flows go under `{{%CORE_IMPLEMENTATION_LAYER_PATH_OR_IDENTIFIER}}`; domain extensions, business capabilities, plugins, models, special algorithms, or feature packages go under `{{%DOMAIN_EXTENSION_LAYER_PATH_OR_IDENTIFIER}}`.
2. Prefer implementing the smallest correct version first, and first ensure public semantics remain compatible with existing types, commands, protocols, configurations, or data models. Numeric projects then add scalar-correct versions and mathematical semantic verification.
3. Before adding capabilities or algorithms, search and evaluate nearby modules, base capabilities, and existing public entries. Numeric or DSP projects must also evaluate existing implementations of base mathematics, vectors, filters, frequency-domain utilities, and similar capabilities.
4. Preallocate coefficients, state, cache, workspace, or LUTs during construction; reuse them during processing.
5. Connect `{{%DATA_PARALLEL_ACCELERATION_BACKEND}}` only when necessary, while preserving macro guards, scalar fallback, and tail handling.
6. If outward exposure is needed, complete the neighboring module's existing matrix of public entry groups, functional API families, command families, endpoint groups, configuration families, data-format families, or similar public entries. C/C++ native library projects must also complete `{{%PRIMARY_LANGUAGE}}` public semantics and installed-header compatibility assessment.
7. When the project uses automatic source collection, recursive file discovery, generated lists, or build-system helper functions, newly added source code is included in the build by `{{%SOURCE_COLLECTION_RULE_OR_HELPER_FUNCTION_NAME}}` only after `{{%BUILD_SYSTEM}}` is reconfigured. Public declarations, test entry registration, and documentation updates still need to be completed explicitly. If the project does not use automatic collection, new files must be explicitly registered according to the real build entry.
8. After C/C++ C linkage wrapper definition matrixization, verify that public declarations have not been macroized, reordered, or modified; generated definitions match public declarations item by item; exported symbols, calling conventions, `{{%ALIAS_RESTRICTION_MACRO_NAME}}` / `const`, error strings, release order, and lifecycles remain unchanged; local matrix macros and all action macros have been `#undef`'d with no macro leakage.
9. Add tests according to the organization style of `{{%MODULE_TEST_FILE_PATTERN}}`, and separate correctness verification from performance observability.

- When generating or modifying code, default to treating inputs as readonly, outputs and mutable buffers as unique write entries, and shared data as shared readonly. Introduce mutable sharing, input/output reuse, in-place processing, or no-alias declarations only when the semantics truly require it, the public contract allows it, and tests cover it.
- General verification dimensions cover at least normal paths, error paths, boundary inputs, permission or access boundaries, missing or conflicting configuration, resource lifecycles, concurrency or reentrancy, compatibility boundaries, migration or rollback paths, and public-entry observable results.
- When an interface declaration prohibits, permits, or requires in-place processing, partial overlap, complete non-overlap, shared readonly access, or unique mutable access, tests must cover the corresponding overlap/non-overlap paths, alias assertions, or contract-failure paths. If they cannot be tested, the risk and to-do plan candidate must state that.
- State modules, sessions, connections, tasks, workflows, or resource objects cover at least initialization, state advancement, reset, continued processing, failure recovery, and invalidation rules after destruction or closing.
- Boundary length, count, pagination, batch size, timeout, quota, time window, capacity, and data range cover at least `0`, `1`, minimum value, maximum value, default value, empty input, single-item input, and input beyond the limit. When a data-parallel backend exists, also cover multiples and non-multiples of the `{{%DATA_PARALLEL_ACCELERATION_BACKEND}}` width.
- Numeric, DSP, graphics, statistical, or approximate-computation projects must additionally cover the genuinely applicable items among zero input, NaN, Inf, tiny values, huge values, impulses, steps, frequency-domain round-trip error, known spectral-line positions, fixed-point overflow, sign boundaries, and shift boundaries. When not applicable, "not applicable" must be marked; these items must not be written as generic default tests.
- Performance tests, log observability, example output, screenshots, menu interaction, or temporary persisted results can only serve as observability and cannot replace correctness criteria, unless the instantiated project has defined them as verification entries and described the limitations.

## 10. Build, Installation, Document Maintenance, Automatic Quality Guard, and Verification

This chapter defines build, installation, document maintenance, and automatic quality guard rules. When the project has a build system, release package, installation artifacts, deployment flow, test entries, generation flow, or resource metadata, the corresponding rules **must be filled in and executed**. When no corresponding flow exists, "not applicable" **must be marked**. CMake, PowerShell, POST_BUILD, GLOB_RECURSE, Windows toolchains, and similar content are only conditional technology-stack facts and cannot be written as default facts for all projects.

- When public entries, API/interfaces, base types, macros, build options, or directory responsibilities are modified, related documents must be updated accordingly. After adding a test module, test command, test page, test script, or test menu, declarations, routes, commands, menu items, optional-range prompts, distribution entries, or automation tasks must be connected according to the instantiated project's real test entries. Projects without headers, menu-style CLIs, or test distribution entries must mark "not applicable" and must not fabricate corresponding structures.
- Ordinary internal source fixes do not need mechanical documentation changes merely because "code changed"; however, once any code, build, or test change makes document facts, boundaries, constraints, or verification processes inaccurate, the corresponding documents must be updated.
- After code facts change, document maintenance should first land in the corresponding responsibility scope of `agents/BASE.md`, `agents/TODO.md`, `README.md`, `AGENTS.md`, and `agents/RULES.md`. Protected content in `README.md`, `AGENTS.md`, and `agents/RULES.md` must follow the project-constraint document hard write gate in this chapter; ordinary document maintenance, ordinary version alignment, Markdown/format repair, six-document alignment proofreading, or automatic quality-domain processes must not bypass it. If the current code fact directly affects published capabilities or public-entry descriptions in the formal user manual, directly related small body text, table rows, notes, a small number of example signatures, version number, updated date, aligned-document fields, or local index entries in `doc/DOCUMENTATION.md` can be updated. This update must not expand into full generation, broad rewrite, full-directory reordering, bulk refreshing of public entries or conditional function-family descriptions, full-book example rewriting, or regenerating a public exposure coverage appendix; if a systematic refresh is needed, `documentation release domain` should be automatically included in the ordinary task.
- Build entries are governed by `{{%MAIN_BUILD_ENTRY}}`, `{{%BUILD_PRESET_FILE}}`, `{{%BUILD_SCRIPT_PATTERN}}`, or an equivalent entry declared by the instantiated project. If the project uses `{{%BUILD_SYSTEM}}`, preset files, language standards, or minimum tool versions, the relationship between `{{%BUILD_SYSTEM_MINIMUM_VERSION_METADATA_FIELD}}` and real tool requirements must be written clearly; a metadata field must not lower the project's actual requirements. Projects without a build system must mark "not applicable".
- When instantiating or maintaining build facts, common automation build scripts, build cleanup scripts, build configurations, CI workflows, and task orchestration entries must be read-only scanned from the controlled project root, and relative scripts, build configurations, and task entry call chains inside the project must be recursively analyzed. File evidence recorded in `agents/BASE.md` can only use relative paths from the controlled project root; task entries may be located as `package.json -> scripts.build`, `Makefile -> clean`, or equivalent. Drive letters, user directories, temporary directories, or other local absolute paths ***must not*** be recorded.
- After adding native source, script entries, platform-related code, runtime extensions, data-parallel backends, or `{{%DATA_PARALLEL_ACCELERATION_BACKEND}}` code, `{{%PRIMARY_LANGUAGE_OR_RUNTIME}}` compile/interpret/package flags, release configuration, debug macros, platform gates, default backend, and parallel runtime conditions must be checked for consistency.
- After modifying source code, public entries, API/interfaces, build scripts, test entries, deployment entries, or installation logic, the instantiated project's full verification entry must be invoked directly for build, packaging, deployment, or equivalent verification: by default run `{{%DEFAULT_FULL_BUILD_SCRIPT}}` or `{{%DEFAULT_FULL_VERIFICATION_COMMAND}}`; if the default toolchain is unavailable, run `{{%FALLBACK_FULL_BUILD_SCRIPT}}` or `{{%FALLBACK_FULL_VERIFICATION_COMMAND}}`. The fallback entry must first be compared with the default entry for coverage, and it must still cover the original `{{%BUILD_TARGET_ARCHITECTURE_COLLECTION}}`, `{{%BUILD_CONFIGURATION_MATRIX}}`, tests, packaging, installation, deployment, or equivalent verification scope. If default and fallback full verification coverage differs, an entry reference is missing, or the fallback entry lacks any part of the original verification scope, it ***must not*** be written as full verification passed; execution must stop and report unverified scope, coverage differences, evidence locations, and recovery entry, and record a candidate issue in `agents/TODO.md` or request user confirmation.
- The full verification flow may first run `{{%BUILD_CLEAN_SCRIPT}}`, then configure, build, test, package, or deploy the `{{%BUILD_CONFIGURATION_MATRIX}}` presets for `{{%BUILD_TARGET_ARCHITECTURE_COLLECTION}}` in order. If cleaning directories such as `{{%AI_TOOL_CONFIGURATION_DIRECTORY}}/`, `{{%IDE_STATE_DIRECTORY}}/`, `{{%IDE_CONFIGURATION_DIRECTORY}}/`, `{{%PACKAGE_DIRECTORY}}/`, `{{%OUTPUT_DIRECTORY}}/`, `{{%BUILD_DIRECTORY}}/`, and `{{%INSTALL_ARTIFACT_DIRECTORY}}/` is project fact, it should be treated as an expected step; this must not be used as a reason to switch to a targeted build or skip full verification.
- When the project uses PowerShell, Windows batch, Shell, Make, CMake, package managers, CI workflows, or other build tools, current working directory, environment initialization, interaction requirements, and permission boundaries must be confirmed before running `{{%FULL_BUILD_SCRIPT_PATTERN}}`. If a script failure path contains `Pause`, an interactive menu, confirmation prompt, or requires manual input and therefore cannot fully execute in a non-interactive environment, the failed step, unverified configuration, and reason must be clearly stated.
- When automatic quality guard or ordinary task verification requires full build verification, the default full build script, fallback full build script, build cleanup script, build configuration, CI workflows, task entries, and their recursive call chains must first be analyzed read-only. If forced closing of file handles, file pointers, objects, locks, processes, IPC resources, or equivalent external resource release operations is found, that step is a dangerous resource-close operation and ***must not*** be executed directly. An equivalent safe full verification path must be used instead, and it must still cover the original `{{%BUILD_TARGET_ARCHITECTURE_COLLECTION}}`, `{{%BUILD_CONFIGURATION_MATRIX}}`, tests, packaging, installation, deployment, or equivalent verification scope; it ***must not*** degrade to a single item, single target, single configuration, local build, or partial test run. If no equivalent safe full verification path can be established, execution must stop and report the dangerous script relative path, dangerous operation type, evidence location, original full verification scope, unverified scope, and recovery entry.
- When no independent `{{%AUTOMATED_TEST_ENTRY_PATTERN}}` flow is currently visible, newly added or extended modules should separate interactive correctness verification from performance observability. Performance printouts, persisted results, menu-input CLIs, manual page actions, or one-off demos must not be treated as replacements for automated tests.
- Tests that need to write files should prefer configurable, relative, or centrally agreed output paths. Personal workspace absolute paths must not keep spreading, and persisted files must not be the sole correctness criterion.
- When only the six controlled documents are modified and source code, public entries, API/interfaces, compatibility boundaries, build scripts, test entries, or installation logic are not touched, full compile/build verification may be skipped, but the final response must clearly state that no build was run and why.
- When the project has default build-target auto-installation, post-build installation steps, or deployment hooks, the relationship between `{{%AUTO_INSTALL_TARGET_NAME}}`, `{{%POST_BUILD_INSTALL_FLOW_NAME}}`, and `{{%INSTALL_ARTIFACT_DIRECTORY}}/` must be written clearly. When project name, export macros, aliases, installation paths, target names, output directories, or public entries are adjusted, final installation artifacts must be checked. Projects without auto-installation or post-build installation flow must mark "not applicable" and must not fabricate installation behavior.
- When version, resource, or installation metadata is modified, resource files and installation artifacts generated by `{{%RESOURCE_DEFINITION_FACT_SOURCE}}` and `{{%INSTALL_ARTIFACT_GENERATION_FACT_SOURCE}}` must be checked. Generated directory content must not be treated as the sole fact source or manual modification target.
- Before modifying code, configuration, scripts, Markdown, or other text files, the encoding, line-ending, EOF-newline, and trailing-whitespace baseline of the text files to be written in this round must first be read and recorded. Changed or newly created Markdown (`.md`) files must use UTF-8 BOM encoding and CRLF line endings, contain no bare LF, preserve the EOF newline, contain no trailing whitespace, and fix all Markdown format issues except `MD013` long-paragraph warnings. Other existing text files must preserve their original encoding and line-ending format, preserve the EOF newline, and contain no trailing whitespace; other new text files must use UTF-8 BOM encoding and CRLF line endings, contain no bare LF, preserve the EOF newline, and contain no trailing whitespace. Binary files, third-party verbatim files, and untouched historical files are not mechanically rewritten because of this rule. Protected content in the protected three documents must not be rewritten under the name of format closure, line-ending repair, whitespace repair, or Markdown repair.
- Markdown files must run markdownlint or an equivalent Markdown syntax check, and discovered issues must be repaired. Markdown special syntax outside plain text, including but not limited to emphasis, backticks, quotes, tables, lists, code fences, and links, **must observe correct space usage**. Missing required spaces, extra spaces, or incorrect mixed CJK/English spacing must not break Markdown parsing, list hierarchy, table column alignment, emphasis range, or body readability. When maintaining `AGENTS.md`, directory-level/project-level agent rules, or similar project constraint documents, `*...*`, `**...**`, and `***...***` must be used by importance to distinguish default preferences, strong constraints, and red lines / stop conditions. User-facing replies should also use the three emphasis levels by importance: ordinary explanation uses little or no emphasis, important conclusions use `**...**`, and high-risk, stop-confirmation, or non-violable items use `***...***`. **Over-emphasis must not make "everything emphasized equals nothing emphasized"**, and strong constraints must not degrade into un-emphasized ordinary text. The `MD013` line-length rule is not a required repair item by default, but its line-length exemption must not be used to skip any other Markdown syntax, structure, link, table, fence, list, whitespace, or format issue. Markdown/format repair must not bypass the protected-content gate for the protected three documents. If `markdownlint`, `npx markdownlint-cli`, or `npx markdownlint-cli2` exists in the current environment, it must be invoked to check Markdown (`.md`) files; if these tools are unavailable, equivalent text checks must be performed, covering at least encoding, line endings, EOF newline, trailing whitespace, and statically identifiable Markdown format issues other than `MD013`. If local `npx` is available and no dependency downloads or writes to `package.json`, lockfiles, npm configuration, or `node_modules` are required, you may first try `npx --no-install markdownlint-cli`, or invoke the project-selected or equivalent Markdown checker through `npx`. When `npx` is unavailable, would trigger downloads, or fails, the checker-unavailable rule must explain the reason, completed substitute checks, and residual risk.
- `git diff --check` must be one of the final checks for trailing whitespace, whitespace errors, and diff-baseline problems. It cannot replace checks for UTF-8 BOM, CRLF line endings, bare LF, EOF newline, trailing whitespace, or Markdown syntax and format.

The six controlled documents are `README.md`, `AGENTS.md`, `agents/RULES.md`, `agents/BASE.md`, `agents/TODO.md`, and `doc/DOCUMENTATION.md`. When any one of them is modified, responsibility scope, cross-references, and version-alignment status must be checked.

If `BOOTSTRAP.md` physically coexists at the same level as the six controlled documents, it exists only as a one-time startup file before instantiation. This statement is only a prohibitive boundary declaration; physical colocation ***must not*** cause it to be included in the six controlled documents, version alignment, fixed protocol fields, cross-reference chain, default load rules, `document quality domain`, `documentation release domain`, fact sources, or later maintenance queue.

| Document | Responsibility Boundary |
| --- | --- |
| `README.md` | Only carries the project overview, capability-boundary summary, usage entries, and document index. |
| `AGENTS.md` | Only carries the agent control entry, automatic quality guard, unobtrusive quality guard, load order, document priority, version rules, plan management entry summary, and high-level red lines. |
| `agents/RULES.md` | Only carries engineering rules, coding-style constraints, document maintenance rules, task plan gates, underlying fact derivation protocol, task risk level, automatic quality guard, unobtrusive quality guard, automatic quality loop rules, task orchestration rules, and formal user manual writing rules jointly followed by developers and agents. |
| `agents/BASE.md` | Only carries the current factual baseline, directory responsibilities, build and installation facts, test entry facts, and current capability status. |
| `agents/TODO.md` | Only carries future implementation plans, known issues, priority, task risk level, automatic quality-loop level, source quality domain, prerequisite domain status, acceptance status, risk dimension, evidence location, first action, and verification recommendation. |
| `doc/DOCUMENTATION.md` | Only carries the formal user manual released to users, and does not carry writing rules, generation rationale, maintenance flows, QA checklists, internal rules, or material-source descriptions. |

Whenever the six controlled documents are referenced in any controlled document, maintenance-entry document, or cross-reference scenario among the six controlled documents, the full relative path with backticks must be used: `README.md`, `AGENTS.md`, `agents/RULES.md`, `agents/BASE.md`, `agents/TODO.md`, `doc/DOCUMENTATION.md`; only file names, short names, bare paths, directory names, or paths without backticks must not be used.

The six-controlled-document cross-reference list ***must not*** be extended to `BOOTSTRAP.md`. When the physical colocation boundary needs to be stated, it may only express the prohibitive boundary excluding seventh-document status, and must not expand instantiation flow, introduce new runtime rules, or form a user-operable quality entry.

Detailed writing rules for `doc/DOCUMENTATION.md` are governed by Chapter 13, "Formal User Manual Writing Rules", in this file. When the manual body is fully generated or broadly rewritten through `documentation release domain`, the automatic quality-domain process in Chapter 12 must also be followed. When directly related small body-text alignment is performed because code facts changed, or when a small erratum, limited local revision, or version number, updated date, and aligned-document field update is performed through a user-explicit manual revision task, the document responsibility boundaries, version alignment, project-constraint document hard write gate, and verification rules in this chapter must also be followed.

`README.md`, `AGENTS.md`, `agents/RULES.md`, `agents/BASE.md`, and `agents/TODO.md` remain one-way transparent to `doc/DOCUMENTATION.md`: the first five documents only provide entries, execution rules, engineering constraints, factual boundaries, and future plan constraints for the formal user manual; `doc/DOCUMENTATION.md` must not define the rules, responsibilities, facts, priorities, or code status of the first five documents in reverse.

When `incremental difference domain`, `incremental security domain`, `factual boundary domain`, `document quality domain`, `public impact domain`, `global security domain`, `static analysis domain`, or `documentation release domain` touches Chapter 13 of this file or protected content in the protected three documents, it must not actively compress, summarize, delete, or weaken content on the grounds of simplification, deduplication, readability improvement, manual alignment, documentation release result, ordinary version alignment, Markdown/format repair, or six-document alignment proofreading. Except for version number, updated date, aligned-document fields, index alignment, or user-explicit rule revision, `documentation release domain` should not rewrite Chapter 13 rule body text. If such modification is truly needed, the rule-fidelity and anti-weakening gate at the beginning of Chapter 13 must first be executed; when protected content in the protected three documents is involved, the project-constraint document hard write gate in this chapter must also be executed.

The above six controlled document names, the eight automatic quality domains, `Test Build Rule`, `explore`, and `general` are fixed protocol constants for the document maintenance framework. During generalization, backfill, compression, rewriting, simulated backfill, templating, or cross-project adaptation, they ***must not be placeholderized, renamed, translated, split, or merged***.

When `explore` and `general` are fixed protocol constants, they must be preserved literally. When they are operational subagent types in task orchestration, `explore` or a subagent type with equivalent read-only capability may be used, and `general` or a subagent type with equivalent read/write capability may be used. Equivalent type names only represent capability adaptation in the current execution environment and ***must not translate, replace, or delete*** `explore` and `general` in the fixed protocol constant list.

`task risk level` and `automatic quality-loop level` are schema field names for task plans, reports, and to-do plans. They are not counted among the above fixed protocol constants, and they must not be written as new user entries. Whenever these two fields are used in plans, reports, quality-loop records, or `agents/TODO.md`, the field names must be preserved literally and must not be renamed, translated into another variant, placeholderized, split, or merged.

`Test Build Rule` is a load-verification protocol constant used only to confirm that the agent has loaded the current control rules and summary. This phrase **must not be renamed, placeholderized, or translated into another variant**, and must not be taken over by build/test entries, automatic quality guard, or template placeholder logic.

Unified rule-load test recognition rule: only `Test Build Rule` can start the rule-load test as an independent complete message. Before recognition, only leading/trailing whitespace and transport-layer line breaks may be removed; after trimming, the message must be exactly equal to that phrase. The eight automatic quality domains must not be written as user-operable entries, independent invocation phrases, phase-selection entries, or quality tasks that users can operate separately.

`Test Build Rule` triggers if and only if the user sends `Test Build Rule` as a complete standalone message. After a hit, the agent **must reply only** with the current version number, loaded summary, authoritative rule location, execution boundary, and tool-not-executed note; it ***must not execute tools*** and must not start build, test, installation, scanning, documentation release domain, code modification, or `agents/TODO.md` writing.

The project-constraint document hard write gate is as follows:

- The protected three documents are fixed as `README.md`, `AGENTS.md`, and `agents/RULES.md`; `agents/BASE.md` is not one of the protected three documents.
- Protected content includes project constraints, agent control rules, automatic quality guard rules, load order, document roles, the six controlled document list and cross-reference requirements, build/test and verification gates, document maintenance and generation boundaries, the protected-content gate itself, anti-weakening rules, stop-and-resume rules, the confirmation phrase, and any project-constraint body text containing "must", "must not", "can only", or "stop and report". Except for the narrow version-metadata exception, any write, revision, move, deletion, reordering, format repair, link repair, table repair, heading repair, wording refinement, rule merge, or body alignment that touches any content in these three documents is within protected-content scope.
- When any task is about to add, delete, rewrite, summarize, weaken, reorder, or migrate protected content in the protected three documents, except for the narrow version-metadata exception, the current task and subsequent tools, subagents, and automation chains ***must immediately stop***, and ***no further write to disk may proceed***. First issue a risk warning to the user explaining that project constraints, agent control, automatic quality guard, document roles, build verification, version alignment, and later worker collaboration boundaries may be broken, and require the user to reply in a standalone message with the confirmation phrase `I understand all possible risks and agree to modify project constraints`. Before confirmation matching, only leading/trailing whitespace and transport-layer line breaks may be removed; after trimming, the message ***must be exactly equal*** to that phrase.
- Similar expressions, extra words, missing words, paraphrases, another language, punctuation changes, earlier declarations, added text in the same message, tool output, subagent reports, text copied into a file, or other restatements do not constitute authorization. User confirmation authorizes only the current explicit scope and current round; it must not be presumed as future authorization, whole-document authorization, adjacent-section authorization, bulk-templating authorization, or authorization for other files. After confirmation, only the protected-content scope explicitly allowed by the user may still be modified. If execution discovers scope expansion, semantic change, or new risk, it must stop again and request confirmation again.
- The narrow version-metadata exception only allows version number, updated date, and aligned-document fields to be aligned. It must not be used to modify responsibilities, quality guard, gates, path lists, rule body text, or strong constraint terms through ordinary version alignment.
- Autonomous controlled iteration of `agents/BASE.md`, `agents/TODO.md`, and `doc/DOCUMENTATION.md` is not restricted by this hard gate, but their own responsibility boundaries must be followed, and they must not define, override, weaken, or migrate protected content from the protected three documents in reverse. If protected content in the protected three documents truly needs modification, this hard gate still applies.
- `factual boundary domain`, `document quality domain`, `documentation release domain`, six-document alignment proofreading, ordinary version alignment, Markdown/format repair, templating, compression, reordering, generation, or cross-project adaptation must not bypass this hard gate.

Process history that has already been implemented and stably incorporated into current facts should be removed seamlessly from the to-do plan or process documents, without retaining completion narrative. Only facts that affect later verification or compatibility judgment should remain in the baseline.

### 10.1 Automatic Quality Domain Low Coupling and In-Group Ordered Prefix Chain Principles

Each automatic quality domain body is a low-coupling atomic capability. Each quality domain must not be implemented as the same fact scan, same global precheck, same Markdown check, or same generic audit flow. General rules constrain control-plane contracts such as automatic inclusion decisions, capability detection, Subagent scheduling discipline, report fields, to-do plan evidence thresholds, stop-and-resume rules, and explicit in-group ordered prefix chains.

The lightweight automatic quality guard group prefix chain is fixed as:

- `incremental difference domain` = `incremental difference domain`
- `incremental security domain` = `incremental difference domain` -> `incremental security domain`
- `factual boundary domain` = `incremental difference domain` -> `incremental security domain` -> `factual boundary domain`
- `document quality domain` = `incremental difference domain` -> `incremental security domain` -> `factual boundary domain` -> `document quality domain`

The full automatic quality guard group prefix chain is fixed as:

- `public impact domain` = `public impact domain`
- `global security domain` = `public impact domain` -> `global security domain`
- `static analysis domain` = `public impact domain` -> `global security domain` -> `static analysis domain`
- `documentation release domain` = `public impact domain` -> `global security domain` -> `static analysis domain` -> `documentation release domain`

When a downstream quality domain is automatically included in the current ordinary task, all chain levels from the first level of its group through the target quality domain must be serially covered according to the prefix chain. Chain levels must not run in parallel, skip levels, or use downstream tasks to backfill upstream conclusions. If an upstream level fails, blocks, stops because of a hard cap, lacks evidence and needs user adjudication, or would touch a safety red line if continued, execution must stop at the current chain level and report the remaining chain levels; downstream levels must not start.

Each chain-level task must independently establish a task brief, subagent orchestration, report, acceptance, and to-do plan candidate boundary. File lists, public exposure lists, Markdown file lists, or other read-only input lists produced by upstream levels may be reused in downstream levels in the same round, but the source, time, coverage scope, and unreused items must be marked. Upstream judgment conclusions, finding lists, acceptance results, or to-do plan candidates must not directly replace downstream primary checks, summaries, reviews, or acceptance.

Each chain level in the full automatic quality guard group must embed the corresponding lightweight chain-level capability domain in its own task brief and acceptance: `public impact domain` strictly includes the incremental risk coverage of `incremental difference domain`; `global security domain` strictly includes the diff security regression coverage of `incremental security domain`; `static analysis domain` strictly includes the factual boundary, responsibility consistency, capability status, and protected-three-documents unauthorized-change risk coverage of `factual boundary domain`; `documentation release domain` strictly includes the six-document alignment verification capability of `document quality domain`. This embedded coverage belongs only to the full quality domain's own check domain, does not constitute cross-group rerun, must not be written as rerunning the lightweight quality domain, and must not use lightweight quality-domain conclusions to replace the full quality domain's primary responsibilities, report, or acceptance.

When multiple quality domains are included by the same ordinary task risk at the same time, first establish task briefs and prefix chains according to the highest target quality domain in each group. Multiple targets in the same group are merged into the longest prefix chain and produce independent reports level by level; cross-group targets establish lightweight and full chains separately. Cross-group chains do not set prerequisites for each other. They may only reuse completely identical and still-fresh read-only input lists from the same round, such as the same Git diff file list, public exposure list, or Markdown file list, and must not reuse them as generic cross-quality-domain conclusions.

Any quality domain may consume fact lists explicitly provided by the user or just produced in the same round, but its own report must mark reuse source, reuse scope, unreused items, and task domains that still require independent checking. If the same issue is found by multiple quality domains, retain only the difference in quality-domain perspectives in the report. When writing to `agents/TODO.md`, deduplicate and merge evidence sources instead of registering the same to-do plan repeatedly.

Issues found by any quality domain must not be repaired through unauthorized modification of source code, public headers where applicable, build scripts, test entries, installation logic, or compatibility boundaries. Documentation-style public entries can only be revised in small, lawful scope within the corresponding quality domain's authorization, and must not use this to change code facts or fabricate public capabilities. All issues must be reported; confirmed issues that have evidence location, impact scope, and first action and need later handling should be automatically submitted to `agents/TODO.md`.

The authoritative field list for `agents/TODO.md` is: ID, priority, task risk level, automatic quality-loop level, source quality domain, prerequisite domain status, acceptance status, risk dimension, issue description, evidence location, impact scope, current exposure surface, first action, verification recommendation, and status. Issues for which the automatic quality loop is not applicable must also explicitly state "not applicable" or an equivalent status; fields must not be omitted. Low-confidence items, tool uncertainties, unlocatable guesses, and pure tool noise remain only in reports and are not mechanically written into the to-do plan.

### 10.2 task risk level and Automatic Quality Loop

The automatic quality loop is an embedded quality-management flow in the ordinary task lifecycle, not a user entry. It must automatically select the chain-level responsibilities, sequence, task briefs, subagent orchestration, report fields, and acceptance rules for either lightweight automatic quality guard mode or full automatic quality guard mode, but must not form a manual quality checklist and must not become a quality task users can invoke separately; `Test Build Rule` is retained only as a rule-load test item.

#### 10.2.1 Plan Management Details

##### Clarification Protocol

- **Ordinary tasks that are complex, high risk, or whose blocking issues have not converged must first clarify underlying facts, goals, scope, confirmation items, and stop conditions in one concentrated pass.**
- **Clarification questions must be short, concrete, and focused on the current blocking point.**
- **Progress must not be delayed by asking only one independent question at a time.**
- **Non-blocking clarification must not replace verifiable action.**

##### Clarification Steps

1. **Restate the result the user wants to achieve, rather than merely restating the method the user proposed.**
2. **Summarize known facts, key assumptions, hard constraints, adjustable preferences, and success criteria.**
3. **Determine whether the current approach is merely a convention or surface-level solution, and return to underlying facts to derive it again when necessary.**
4. **List issues blocking execution, mandatory user-confirmation items, and stop conditions.**
5. **Ask all currently known blocking questions together in priority order.**
6. **Do not ask only one question at a time unless a later question depends on an earlier answer.**
7. **After the user answers, recheck blockers, explicit assumptions, risk level, read/write ownership, and `automatic quality-loop level`.**
8. **When no blockers remain, output the execution plan and continue.**

##### Plan Confirmation Requirements

- ***High-risk operations, protection gates, Git, external resources, sensitive files, dependencies, databases, deployment, or release actions must not be executed until current explicit user authorization is obtained or a narrow exception defined by the rules applies.***
- **Execution plans for complex ordinary tasks and high-risk ordinary tasks must first cover the goal, scope, constraints, risks, verification, and rollback before implementation proceeds.**
- **Plan text, historical requests, template body text, or automatic quality guard must not constitute authorization across tasks, rounds, outside the scope, or for high-risk operations.**
- **When risk judgment cannot be made reliably, full automatic quality guard mode must be selected; if full automatic quality guard mode is still insufficient to explain conflict, permission, or responsibility boundaries, execution must stop and request user adjudication.**

##### Plan Fields

- **Task-risk fields**: `task risk level`, judgment evidence, `automatic quality-loop level`, inclusion reason, task complexity/scale assessment, blocking-issue check result, and confirmation status.
- **Boundary fields**: Git/worktree baseline, safety and sensitive-information boundary, mandatory user-confirmation items, rollback method, recovery entry, stop conditions, and acceptance output.
- **Orchestration fields**: expected chain levels, subagent orchestration, capability detection time point, dynamically detected actual concurrency cap, hard total cap, detection-failure stop action, and main-agent context retention scope.
- **Index fields**: code-index capability status, index-result usage boundary, and index-failure fallback method.
- **Dependency fields**: task dependency graph, explicit dependencies, implicit dependencies, cycle-dependency check result, document read/write ownership, file responsibility boundary, per-file responsibility matrix, and parallel delegation strategy.
- **Verification fields**: verification method, verification entry, failure handling method, and final-report acceptance criteria.

##### Plan Content

- **Complex/high-risk task plans must include the goal.**
- **Complex/high-risk task plans must include the scope.**
- **Complex/high-risk task plans must explicitly state what will not be done.**
- **Complex/high-risk task plans must include underlying facts and key assumptions.**
- **Complex/high-risk task plans must include the rationale for the approach derived from underlying facts.**
- **Complex/high-risk task plans must include implementation steps.**
- **Complex/high-risk task plans must include parallelization opportunities and task dependencies.**
- **Complex/high-risk task plans must include risks.**
- **Complex/high-risk task plans must include verification methods.**
- **Complex/high-risk task plans must include rollback methods.**
- **Complex/high-risk task plans must include stop conditions, acceptance outputs, and controlled recovery entries.**
- **Plans retain only executable boundaries, changes, verification items, stop conditions, and reporting requirements.**
- **Historical process restatements, unverifiable old assertions, stale line numbers, generalized risk descriptions, or out-of-scope freeze/release conclusions must not be written as implementation instructions.**
- **Line numbers can only serve as supporting evidence; before implementation, relevant files, diffs, or search results must be rechecked against the current worktree.**

##### Plan Confirmation Gate

###### Applicability

- **Complex ordinary tasks, high-risk ordinary tasks, or ordinary tasks requiring user confirmation must not begin implementation before the plan passes inspection.**

###### Checklist

- **Is the requirement background known?**
- **Is the final goal clear?**
- **Do inputs and outputs have clear boundaries?**
- **Is there any conflict with real conditions?**
- **Does any unresolved implicit assumption remain?**
- **Is any detail still missing or improper?**
- **Does any remaining blocker affect plan execution?**
- **Does any unrelated noise outside the current requirement remain?**

###### Stop Conditions

- ***If any checklist item remains vague, ambiguous, contradictory, noncompliant, or affects execution, it must be listed immediately and confirmation must be requested.***
- ***A complex or high-risk plan must not continue on the unconfirmed premise that a key assumption is true.***
- **Unrelated noise must be removed from the plan, implementation, acceptance, and report scope and must not be used as an execution basis.**
- **Large refactoring, adding/upgrading/removing dependencies, unrelated interface-signature or public-contract changes, module-structure migration, bulk renaming, or other high-impact actions beyond the current task boundary must be listed under `mandatory user-confirmation items`.**

###### Low-Risk Exception

- *For small low-risk, reversible, clear-scope tasks, do not over-apply the complete plan confirmation gate; complete them directly based on reasonable assumptions, while still preserving enough information about the goal, key assumptions, and verification results for validation.*

##### Interactive Review

- **When the user explicitly requests plan review, interactive review, that the plan not yet be implemented, or item-by-item inspection of plan deviations, implementation must pause and the interactive-review process must begin.**
- **Interactive review must use the plan-review confirmation points above and the current plan details to recheck deviations, conflicts, implicit assumptions, omitted details, remaining blockers, and unrelated noise.**
- **Interactive review must first distinguish independent blocking questions that can be clarified together from confirmation points requiring item-by-item adjudication. Independent blocking questions remain subject to the clarification steps and are asked together. Only when the user explicitly requests item-by-item inspection, dependencies exist among confirmation points, or single-point confirmation is necessary to reduce high-risk misconfirmation may only one confirmation point be asked per round in risk-priority order, together with an evidence summary, risk judgment, suggested options, and recommended option, or with an explicit allowance for the user to decide independently.**
- **After the user answers, the remaining confirmation points, blockers, risk level, read/write ownership, and `automatic quality-loop level` must be reassessed before moving to the next item or returning to `PLAN_READY`.**
- ***Interactive review is used only to converge the current ordinary-task plan. It is not a user-operable entry, quality-domain name, or manual chain, and must not change automatic/unobtrusive quality guard semantics.***
- **Non-blocking preference questions must not be packaged as item-by-item confirmations to delay low-risk execution.**

##### Plan Start and Execution Continuity

- **When the user explicitly signals plan start; the context, codebase, version baseline, dependency environment, and necessary test environment have been confirmed ready; all plan-review confirmation points and blockers have been cleared; and no security, permission, sensitive-information, Git, external-resource, database, production-environment, protection-gate, or user-confirmation boundary is triggered, implementation must begin strictly according to the established plan orchestration.**
- **After a plan starts, execution must continue until the plan's final goal is achieved, verification passes, or a controlled stop condition is triggered.**
- **Context compaction, turn changes, completion of staged subtasks, passing local verification, existing partial output, long task duration, or completion of an automatic quality-loop stage must not be used to package an unachieved final goal as a completion conclusion.**
- **When an ordinary, locatable verification failure occurs during execution and can be repaired safely within the current authorization, its cause must be analyzed, the minimum repair implemented, and verification rerun. Execution may stop under control only when a new blocker is found, the plan basis becomes invalid, capability detection fails, read/write ownership conflicts arise, continuing would cross a confirmation boundary, the verification failure cannot be recovered safely within the current authorization, or continuing would expand risk; the stop report must state completed scope, incomplete scope, blocking reason, recovery entry, and the minimum next continuation action.**
- ***Execution continuity must not be used to bypass stop conditions, user confirmation, protection gates, or high-risk boundaries.***

##### Engineering Implementation Loop

- **Medium or complex implementation tasks must continuously follow the loop "observe and gather evidence → clarify goals and constraints → formulate or adjust the approach → implement the minimum relevant change → perform verification → analyze results → repair and reverify when necessary".**
- **Each round of requirement decomposition, solution planning, task orchestration, implementation, and verification must take as input the current decision baseline composed of the real goal and success criteria, verified facts, hard constraints, assumptions to verify, adjustable preferences, and risks. Conventions, historical approaches, tool capabilities, or concurrency convenience must not determine goals, requirements, approaches, or task boundaries in reverse.**
- **Before each round begins, the current decision baseline must be refreshed from current source code, worktree state, tool output, and the latest verification results; invalid assumptions, stale conclusions, or the previous round's state must not continue to be relied upon.**
- **Requirement decomposition must break the real goal into independently acceptable requirements and bind each one to its output, scope and non-goals, success criteria, constraints, key assumptions, evidence, and prerequisites. Steps that cannot be traced to the real goal must not enter the plan.**
- **Solution planning must identify for each candidate approach its supporting facts, key assumptions, applicability conditions and falsification conditions, satisfied requirements, tradeoffs, and verification method. When several approaches can all satisfy the goal and hard constraints, prefer the one with fewer key assumptions, smaller impact, reversibility, and verifiability.**
- **Task orchestration must derive the task graph from requirements, fact acquisition, data and control dependencies, read/write ownership, verification paths, and acceptance dependencies. When new evidence changes a premise, the task graph and execution order must be updated before continuing; concurrency capability determines only the safe upper bound for nodes suitable for parallel execution.**
- **Verification must form a traceable relationship of "requirement or key assumption → verification action → current evidence → conclusion", distinguish confirmed facts, rejected assumptions, and still-unknown items, and feed them back into the current decision baseline. Approaches, steps, and conclusions that depend on invalid assumptions must be withdrawn and derived again. Persisting stable project facts to `agents/BASE.md` remains subject to document responsibilities and current write authorization; process evidence must not be persisted as project fact.**
- **When verification fails, the cause and its relevance to the current task must first be located. Relevant failures must enter the next round of analysis, minimum repair, and reverification; unrelated old issues can only be reported and must not expand task scope without authorization.**
- **Every round of changes must remain minimal, explainable, verifiable, and reversible, and must not overwrite existing changes by the user or other tools.**
- **Task completion requires all of the following simultaneously: the goal and success criteria have been achieved; every key assumption affecting correctness, boundaries, or acceptance is supported by evidence or proven not to affect the conclusion; all applicable verification has passed; related failures have been resolved; the final diff matches expectations; and no unreported blockers remain. If any key assumption still lacks that evidence, the task must not be judged successfully complete. After local verification passes, the final regression verification allowed by the current scope must be run and the final diff rechecked. Completion must not be declared early because the first implementation round finished, one test passed, or an unverified subjective judgment was made.**
- **When consecutive loops make no effective progress, the goal, facts, assumptions, approach, and verification entry must be rechecked; mechanically repeating the same failed operation is prohibited.**
- **A controlled stop is allowed only when a new blocker is found or the plan basis becomes invalid and cannot reconverge within the current authorization, capability detection fails, a read/write ownership conflict arises, continuing would cross a confirmation boundary, necessary permission is missing, the environment is unavailable, key input is missing, a security or high-risk boundary is triggered, a verification failure cannot be recovered safely within the current authorization, or continuing would cause unacceptable harm. The stop report must include completed scope, incomplete scope, failure evidence, current blocker, recovery entry, and the minimum next action, and a controlled stop must not be marked as successful completion.**

The engineering implementation loop is an automatic and unobtrusive discipline embedded in the ordinary task lifecycle. It is not a user entry, quality-domain name, independent invocation phrase, or manual chain; it does not bypass automatic quality-strength judgment and does not broaden the narrow `Test Build Rule` exception.

##### Verification and Final Report

- **Verification after plan execution must tie back to the plan goal, success criteria, explicit assumptions, non-goal scope, risks, stop conditions, rollback boundary, and `automatic quality-loop level`.**
- **When verification cannot be executed, the reason, impact scope, and verification commands the user can run must be stated.**
- **When verification fails, the engineering implementation loop above must first locate and route the cause: ordinary, locatable failures that can be repaired safely within the current authorization continue through minimum repair and reverification, and execution stops only when a controlled stop condition is met. Failed verification or a controlled stop must not be packaged as a completion conclusion.**
- **The final report must distinguish completed scope, incomplete scope, verification results, remaining risks, to-do plan candidates, user-adjudication items, and recovery entry.**

#### 10.2.2 Underlying Fact Derivation Protocol

Underlying fact derivation is a general planning discipline embedded in the ordinary task lifecycle. It is not a user entry, not a manual quality-stage selector, must not restore a user-manual-trigger quality command model, and must not let the eight automatic quality domains become quality tasks users can invoke separately. It spans and constrains the entire process of requirement decomposition, solution planning, task orchestration, implementation loops, validation rollback, and final acceptance; it must be embedded in the ordinary task's planning, implementation, verification, and report, and must preserve automatic/unobtrusive quality guard semantics.

Ordinary tasks that are complex, medium/high risk, unclear in goal, based on a surface-level user-proposed solution, contain key assumptions, or require subagent orchestration must enter the following internal state machine. Simple low-risk tasks with clear scope may be executed directly, but unverified assumptions still must not be written as facts:

| State | Meaning | Allowed Actions |
| --- | --- | --- |
| `INTAKE` | Receives the user goal, constraints, or surface-level solution. | Identify task type, risk, scope, and whether blockers exist. |
| `DECOMPOSE` | Decomposes underlying facts. | Distinguish the real goal, underlying facts, hard constraints, unverified assumptions, experience-based solutions, adjustable preferences, and risks. |
| `CLARIFY` | Blockers have not yet been cleared. | Ask the minimum necessary clarification questions in one concentrated pass, or request user confirmation for explicit assumptions that affect the plan. |
| `DESIGN` | Blockers have been cleared or no longer block progress. | Compare candidate approaches and explain adopted and rejected reasons. |
| `PLAN_READY` | The plan is ready to execute. | Output the executable plan, verification method, risks, stop conditions, and rollback method. |
| `EXECUTE` | Implements according to the plan. | Modify only within the authorized scope, without expanding file, interface, Git, or external-resource boundaries. |
| `VALIDATE` | Verifies and rechecks. | Tie back to the goal, success criteria, explicit assumptions, out-of-scope items, and automatic quality-loop result. |
| `CLOSED` | The task is complete or has stopped under control. | Output final result, verification evidence, remaining risk, to-do plan candidates, and recovery entry. |

Underlying fact decomposition records at least the following categories. If a category is not applicable, it must be explicitly marked not applicable in the plan or execution summary; unknowns that affect the route must not be silently omitted:

| Category | Definition | Handling Rule |
| --- | --- | --- |
| Real goal | The final result the user wants to achieve, which is not necessarily the first proposed method. | Complex tasks must first recover the goal and success criteria. |
| Underlying facts | Verified or not freely changeable facts that determine the essence of the problem. | Use them as approach-derivation inputs; when evidence is insufficient, do not write them into acceptance conclusions. |
| Hard constraints | Safety, permission, platform, interface, data, resource, release, Git, compatibility, or responsibility boundaries. | Directly constrain the plan, stop conditions, and rollback method. |
| Unverified assumptions | Information inferred by the session agent but not yet confirmed. | Clarify or request confirmation when they affect route, boundary, or acceptance. |
| Experience-based solution | A common but not necessarily correct solution. | Use only as a candidate, and inspect applicability conditions and rejection reasons. |
| Adjustable preference | A choice the user wants but has not declared as a hard constraint. | Should not block low-risk execution; note key assumptions in the final report. |
| Risk | A factor that may cause wrong results, irreversible impact, security issues, or verification failure. | Must enter the plan, stop conditions, verification, and report. |

If an unknown changes algorithm route, interface design, implementation architecture, performance target, security boundary, data boundary, Git/release action, read/write ownership, subagent orchestration, automatic quality guard fidelity, or acceptance method, it is a blocker. While blockers remain uncleared, the task ***must not*** enter `PLAN_READY`, `EXECUTE`, or the final execution plan; it may only continue clarifying, declare explicit assumptions, request user confirmation, or stop and report.

Minimum necessary clarification must raise all currently known blocking questions in one concentrated pass. Each question must directly map to an underlying fact or hard constraint and state the plan decision it affects. After the user answers, blockers, explicit assumptions, risk level, read/write ownership, and `automatic quality-loop level` must be checked again. A single answer must not be interpreted as authorization across tasks, protected three-document authorization, Git authorization, release authorization, or future authorization.

Before entering `PLAN_READY`, each item must be confirmed: real goal is clear, scope and non-goals are clear, target object or inputs/outputs are clear, key underlying facts are clear, key assumptions are confirmed, explicitly declared, or judged non-blocking, the approach route has applicability basis, file/module impact scope and read/write boundaries are clear, test and acceptance standards are clear, risks, stop conditions, and rollback method are clear, and high-risk actions have received required authorization or are allowed by a narrow rule exception. If any item is not satisfied, the task must remain in `CLARIFY` or `DESIGN`, and the final execution plan must not be output.

Complex/high-risk ordinary-task plans include at least: task goal, scope and non-goals, underlying fact decomposition, confirmed facts, explicit assumptions and verification methods, assumptions not adopted or rejected, blocker-clearance explanation, candidate approach comparison, recommended approach and derivation reason, file/module impact scope, implementation steps, test and acceptance plan, performance or quality metrics, risks/stop conditions/rollback method, and execution-gate conclusion. Simple low-risk tasks do not have to expand all items, but must preserve enough goal, key-assumption, and verification-result information for validation.

The acceptance stage must tie back to the user's real goal, success criteria, explicit assumptions, non-goal scope, automatic quality-loop result, and stop conditions. If verification fails, subagent conclusions conflict, new blockers are discovered, or plan basis becomes invalid, the task must return to `DECOMPOSE`, `CLARIFY`, or `DESIGN` to converge again; failed verification must not be packaged as a completion conclusion.

`task risk level` is judged strictly:

| task risk level | Applicable Conditions | automatic quality-loop level |
| --- | --- | --- |
| Low risk | Clear-scope local text, comments, low-coupling implementation, or small factual alignment that does not change public entries, API/ABI, build/test entries, installation/release, security boundaries, version rules, automatic quality guard, core semantics of the protected three documents, or user promises. | Lightweight automatic quality guard mode |
| Medium risk | Local document or code changes have clear scope but may affect factual consistency, document accuracy, incremental security domain, test explanations, to-do plan, or neighboring-module understanding. | Lightweight automatic quality guard mode; if the impact expands, escalate to full automatic quality guard mode |
| High risk | Modifies or may affect public entries, API/ABI, compatibility, security, build/test, installation/release, data formats, configuration formats, protocols, systematic formal user manual content, release-freeze conclusions, core semantics of the protected three documents, automatic quality guard system, subagent orchestration, documentation release rules, formal user manual rules, quality gates, or project instantiation flow. | Full automatic quality guard mode |
| Indeterminate | Fact sources conflict, impact scope cannot be narrowed, risk evidence is insufficient, the user explicitly requests a full/careful/final review, a pre-freeze final lock is requested, or continuing would create an unconfirmed tradeoff among automatic quality guard, document responsibilities, and protected gates. | Full automatic quality guard mode; if the full chain is still insufficient to explain conflict, permission, or responsibility boundaries, stop and request user adjudication |

The lightweight automatic loop must run serially as `incremental difference domain` -> `incremental security domain` -> `factual boundary domain` -> `document quality domain`. The full automatic loop must run serially as `public impact domain` -> `global security domain` -> `static analysis domain` -> `documentation release domain`. Each chain level remains an independent task and must have an independent task brief, capability detection, subagent orchestration, report, acceptance, and to-do plan candidate boundary. When an upstream level has not been accepted, fails, blocks, is interrupted by a hard cap, lacks subagent capability, discovers a need for out-of-scope writing, or requires user adjudication, the downstream level must not start.

When implementing a task plan, after the implementation stage is complete, the corresponding quality chain must be automatically orchestrated and executed according to the `automatic quality-loop level` in the plan. The task must not be judged finally complete before that quality chain completes acceptance, and the chain must not be skipped because the implementation stage is already complete, the change is small, time is insufficient, context compacted, human review already occurred, or tool results already exist. Read-only checks in the automatic loop use `explore` or a subagent type with equivalent read-only capability; write repairs, to-do plan recording, version-field alignment, or merge drafting use `general` or a subagent type with equivalent read/write capability. Concurrency is allowed only among subtasks inside the same chain level that have no explicit dependency, no implicit dependency, no cyclic dependency, no write conflict, and no document read/write ownership conflict. The actual concurrency cap is the current environment's real available subagent concurrency cap confirmed by capability detection at the beginning of that chain level. Chain levels must be serial. If the concurrency cap cannot be reliably detected, real subagent capability is unavailable, the dependency graph cannot converge, or ownership conflicts cannot be isolated, execution ***must stop and report***.

An automatic quality-loop chain level itself is part of the current loop. After that chain level completes, it only delivers acceptance results to the next chain level or final report of the current loop, and does not recursively start a new automatic quality loop for that chain level. Only after the current loop as a whole is complete does the final report summarize loop status, remaining risks, and to-do plan candidates.

Independent acceptance is performed by the session agent by default. The session agent must judge pass/fail based on the chain-level task brief, subagent reports, verification results, stop conditions, and to-do plan boundary, then decide whether to enter the next level. Manual confirmation is requested only when user adjudication, exemption, risk acceptance, or a constraint conflict is needed. New issues found by the automatic loop must not be repaired without authorization. Issues that need later handling and meet the field threshold are written or output as to-do plan candidates, while still following the current write authorization boundary and the hard gate for the protected three documents.

Findings from the automatic quality loop must first be routed into automatic repair items, to-do plan candidates, and user-adjudication items. An issue is an automatic repair item only when all of the following are true: it is within the current ordinary-task goal or this round's authorized write scope; its risk level is low, or it is medium risk with sufficient evidence, local impact surface, and a clear repair path; the repair is reversible and verifiable; it does not modify public entries, API/ABI, build/test entries, installation/release boundaries, security boundaries, dependencies, databases, external resources, sensitive files, automatic quality guard system, subagent orchestration, quality gates, protected content in the protected three documents, or user commitments; and it will not overwrite unrelated changes made by the user or other tools. For automatic repair items, the agent **must** execute the minimal repair, targeted verification, and quality-domain back-check within the current authorization by `general` or a subagent type with equivalent read/write capability, and must not hand everything to the user for review by default. Only issues that fail automatic-repair conditions but have sufficient evidence and require later handling are written or output as to-do plan candidates. Only issues involving high risk, risk acceptance, exemptions, factual conflicts, public-contract tradeoffs, protection gates, external resources, or unclear user intent are sent for user adjudication.

When the automatic quality loop conflicts with automatic quality-domain chain definitions, subagent hard constraints, the hard gate for the protected three documents, formal user manual boundaries, or project instantiation flow, execution ***must stop and report***; no unconfirmed tradeoff may be chosen autonomously. The stop report must list completed chain levels, blocking reason, remaining queue, recovery entry, risk level, automatic quality-loop level, and concrete issues requiring user adjudication.

### 10.3 General Capability-Adaptive Orchestration Principles

Before task splitting and parallel delegation, data and control dependencies, read/write ownership, verification paths, and coordination costs must first be clarified. Parallel execution is allowed only when task nodes can be delivered and verified independently and the expected parallelization benefit exceeds the cost of splitting, scheduling, summarizing, and rechecking. Concurrency capability only limits the safe concurrency cap for tasks that pass this gate and ***must not*** drive task splitting in reverse, create unnecessary tasks, or change dependency and acceptance boundaries.

Each quality domain, automatic quality loop, and chain level must first detect whether the current runtime environment has real Subagent Capability, whether nested subagents are supported, the current available real subagent concurrency cap, and whether a hard cap exists on total subagent creation count for this round or session. The actual concurrency cap must be the current environment's available real subagent concurrency cap confirmed by capability detection for that run. Fixed numbers must not be hard-coded, and ordinary parallel tools or single-agent processes must not be used to masquerade as subagent capability. If concurrency capability is probed by actually creating subagents, the first `N` successful subagents only prove that at least `N` are currently supported and must not be claimed as the maximum cap directly. When there is no explicit environment cap, low-risk read-only subagent tasks must be used for incremental, segmented, or equivalent batch probing, and each successful batch can only update the verified available concurrency lower bound. After a failure probing point appears, probing must continue between the last stable success value and the failure point through stepwise, binary, or equivalent interval refinement until an adoptable maximum safe concurrency cap is confirmed, or until further refinement would create resource, context, hard-total-cap, safety, or external-impact risk. If refinement cannot continue, the last stable success value must be adopted as a conservative safe cap, while the unrefined interval, reason for not refining, and remaining uncertainty must be recorded; this conservative value must not be reported as a proven real maximum cap of the environment. If the concurrency cap cannot be reliably detected, detection results conflict with actual creation capability, or real subagent capability is unavailable, execution ***must stop and report***. Capability detection results must be written into the task brief or execution summary, and subjective assumptions must not be used to skip it. Capability detection is a lightweight control-plane action and must not include reading the whole repository, full public-header scans where applicable, Markdown proofreading, project-state sensing, or any quality-domain business check. Business input for a quality domain can only be decided by that domain's own scope.

Planning mode, execution mode, writing phase, validation phase, each quality domain, automatic quality loop, chain level, and continuation recovery phase must each re-detect current real subagent capability, nested capability, available real subagent concurrency cap, and hard total cap. Planning-stage detection results can only be used as a basis for planning feasibility, ordinary task splitting, queueing strategy, and risk assessment; they ***must not*** be inherited, cached, reused, or defaulted as current caps by execution phase, later quality domains, writing phase, validation phase, or continuation recovery phase. Actual concurrency must take the safe minimum of the current phase's re-detected cap, task dependency graph, explicit/implicit/cycle dependencies, file read/write ownership, single write responsibility, chain-level serial requirements, hard gate for the protected three documents, context/resource safety boundary, and user explicit limits. Within that boundary, real subagent tasks that have passed the dependency and benefit gate above, can be split, can run in parallel, and can be independently accepted must be delegated as much as possible. If detection results conflict between phases, execution phase cannot be reliably re-detected, or ownership boundaries cannot be isolated, execution ***must stop and report***, and planning-stage or historical detection caps ***must not*** be reused to continue.

Subagent type selection must be bound to the task access boundary. Subagents specified by the task brief as read-only must use `explore` or a subagent type with equivalent read-only capability. Subagents specified by the task brief as needing modification or file writing must use `general` or a subagent type with equivalent read/write capability. Read-only subagents must not modify the worktree, write `agents/TODO.md`, align version number, updated date, or aligned-document fields, generate temporary drafts, merge drafts, rewrite the formal user manual, or perform any persisted repair. Tasks requiring writing must not be disguised as read-only exploration tasks.

| Task Access Boundary | Required Subagent Type |
| --- | --- |
| Read-only checks, repository exploration, file/function/public exposure list building, fact verification, review, scanning, analysis, summary, and recheck | `explore` or a subagent type with equivalent read-only capability |
| Writing or modifying the worktree, controlled documents, `agents/TODO.md`, version number, updated date, aligned-document fields, section drafts, merged outputs, formal user manual body, allowed repairs, or any persisted artifact | `general` or a subagent type with equivalent read/write capability |

If the same task contains both read-only checks and write modifications, it must be split into `explore` or equivalent read-only tasks and `general` or equivalent read/write tasks. If tool or scheduling limitations make the split impossible, execution ***must stop and report*** that the task-splitting requirement is not met; a single generalized subagent must not complete it by exceeding authorization.

Before orchestrating the eight automatic quality domains, the automatic quality loop, or controlled document maintenance tasks, a task dependency graph must be established. The task dependency graph includes at least explicit dependencies, implicit dependencies, cycle dependency checks, document read/write ownership, file responsibility boundaries, write conflicts, chain-level serial constraints, and hard-gate impact for the protected three documents. Parallel startup is allowed only when the dependency graph proves that tasks inside the same chain level are mutually independent, have no implicit blockers, no cycle dependencies, no read/write ownership conflicts, and no shared write targets. Otherwise tasks must be serialized, split, queued, or stopped and reported.

Each maintained file must have one single writing owner and a read/write barrier. The same file can only be written by one `general` or equivalent read/write task at a time. Before writing, read-only summary and ownership adjudication must be completed; after writing, the session agent or an independent recheck task must verify it. Separate assignment means responsibility boundaries are clear; it does not mean parallelism is required, and it must not permit parallel writing to the same file.

Within the real subagent concurrency cap dynamically detected for that run, tasks that have passed the dependency and benefit gate above, can be split, can run in parallel, and can be accepted independently must be delegated to real subagents as much as possible. The session agent must keep main-session context concise, retaining only task briefs, key findings, acceptance conclusions, blocking reasons, remaining queue, recovery entry, and final-report material. Long evidence, per-file lists, per-work-unit details, and raw observations should preferably be carried by subagent reports. Context concision must not replace independent parent-agent acceptance and must not delete task briefs, queue status, or blocking evidence needed for recovery.

Capability-adaptive architecture is selected in this order:

1. When nested subagents are supported, a three-layer physical architecture must be used: session agent, quality-domain coordinator subagent, and execution/summary/recheck subagents.
2. When only the session agent can split subagents and subagents cannot continue delegation, a two-layer sibling architecture must be used: the session agent acts as a limited scheduler, first starts a quality-domain coordinator subagent to produce the task brief, then starts sibling execution, summary, and recheck subagents according to the task brief.
3. As long as any subagent splitting capability exists, execution ***must not degrade to a single agent*** directly completing the quality domain's primary task.
4. When the actual concurrency cap confirmed by capability detection for that run is reached, the complete task brief must be preserved and tasks must queue in batches. Task count ***must not be reduced***, task domains that should be independently responsible must not be merged into one generalized subagent, and the actual concurrency cap confirmed by detection must not be exceeded.
5. When the hard total cap is exhausted while independent tasks remain incomplete, execution ***must stop and report***, preserving task brief, completed artifacts, incomplete tasks, and remaining queue for continuation.
6. When no real subagent splitting capability exists at all, execution ***must stop and report***, preserving task brief, coverage status, uncovered items, and recovery entry. It ***must not switch to a single agent*** to execute chained primary tasks, and incomplete scope must not be written as complete.

The session agent, parent agent, or quality-domain coordinator must not proactively cancel, terminate, replace, merge, or declare failure for subagents because they run for a long time, temporarily produce no output, progress slowly, wait in queue, or have complex tasks. Incomplete subagents may be ended only when the user explicitly requests cancellation or stop, a platform/tool/session hard cap forces interruption, the subagent itself returns complete/failed/blocked, or continuing would cause an unacceptable safety red line.

When a parent agent performs controlled termination of an incomplete subagent, it must recover and record the subagent's file responsibility, read/write permission, start state, completion state, termination reason, trigger condition, completed scope, incomplete scope, reusable intermediate conclusions, content that cannot be used as acceptance evidence, remaining queue, recovery entry, and minimum next continuation step. Output from an incomplete subagent can only be used as clues or risk hints, and must not be used as a completed result, acceptance conclusion, file-level coverage proof, or freeze basis.

The parent agent must not set arbitrary timeouts that are obviously shorter than task complexity. When tools require timeouts, use the maximum available value or rule-allowed value that permits task completion, and record the limitation in the task brief. When the platform or tool forcibly interrupts, the parent agent must report an incomplete state caused by external limitation, preserve task brief, completed artifacts, incomplete tasks, and remaining queue, and must not write it as complete or privately finish it with a single agent or another task.

Insufficient concurrency can only enter queued waiting, and exhaustion of the hard total cap can only enter stop-and-resume. Neither may be used by the parent agent as a reason to kill long-running subagents, reduce task count, merge independent tasks, or declare incomplete tasks failed.

### 10.4 General Roles, Prohibitions, and Report Fields

| Role | Responsibility |
| --- | --- |
| Session agent | Responsible for automatic inclusion decisions, capability detection, scheduling supervision, boundary communication, and final diff or result audit; it does not directly replace the coordinator or execution tasks for primary work. |
| Quality-domain coordinator | Responsible for reading corresponding rules, establishing task briefs, dividing task domains, defining acceptance conditions, and recording created subagent count, remaining creatable count, queue status, artifact paths, or coverage matrices. |
| Execution task | Handles only one fact domain, document domain, module domain, file group, function family, chapter, or split unit assigned by the task brief; it must not perform unassigned scope. |
| Summary task | Integrates execution-task results only within the current quality-domain task-brief boundary, deduplicates issues, forms lists, and preserves uncovered items; it must not backfill incomplete content as complete. |
| Recheck task | Independently checks task-brief coverage, result consistency, modification boundaries, and Markdown/format, fact, safety, compatibility, or confidentiality boundaries relevant to this quality domain. When gaps are found, it must reassign, fill, queue, or stop for continuation. |

Subagent types for the above roles are selected by access boundary: read-only coordination, execution, summary, and recheck tasks use `explore` or a subagent type with equivalent read-only capability; coordination, execution, summary, or recheck tasks involving writing `agents/TODO.md`, revising documents, generating temporary drafts, merging drafts, review modifications, version alignment, or other persisted actions use `general` or a subagent type with equivalent read/write capability, or are split into `explore`/equivalent read-only tasks and `general`/equivalent read/write tasks.

No quality domain may skip capability detection, task briefs, independent rechecks, queuing, or hard-cap stop-and-resume on the grounds that it is a "lightweight task". Except for prerequisite chain levels that must be run serially because of the explicit ordered prefix chain within its group, no quality domain may perform the primary responsibility of another quality domain, and it must not expand its own required list-building into a cross-group generic precheck.

Each quality-domain final report contains at least: automatic inclusion reason, quality-domain ownership, chain-level ownership, task risk level, automatic quality-loop level, blocking issue handling, user confirmation status, safety/Git boundary, prerequisite chain-level completion or blocking status, embedded lightweight capability-domain acceptance result, capability detection result, detection method, whether an explicit environment cap was used, verified available concurrency lower bound, failure probing point, post-failure interval-refinement result, unrefined interval and reason, adopted maximum safe concurrency cap, actual concurrency allowed by task dependencies, reason for not filling the verified cap when applicable, dynamically detected actual concurrency cap, code-index capability status, index usage scope, index failure fallback method, task dependency graph check conclusion, explicit/implicit/cycle dependency handling, document read/write ownership conflict handling, parallelization-benefit and coordination-cost judgment, reasons tasks did not enter the parallel set, per-file subagent responsibility, parallel delegation status, controlled termination status, incomplete scope, main-agent context retention scope, hard total cap, detection-failure or capability-conflict stop reason, adopted architecture, subagent type assignment, task brief summary, coverage scope, uncovered items, reused list source, finding list, to-do plan write status, reasons for not writing to the to-do plan, verification result, reason for unexecuted verification, recovery entry, and remaining risk. The automatic quality loop uses the inclusion reason from the plan and must not fabricate a user request. Each finding in the finding list contains at least evidence location, impact scope, first action, risk dimension, to-do plan write judgment, task risk level, and automatic quality-loop level. Low-confidence hints that do not meet these fields can only be report notes and must not be fabricated as confirmed issues.

### 10.5 Quality Domain Responsibility Split Table

This table describes each chain level's body responsibility and explicit non-responsibilities. The in-group explicit ordered prefix chain only defines startup order and acceptance gates; it does not change any chain level's responsibility boundary.

| Quality Domain | Independent Responsibility | Explicitly Not Responsible For |
| --- | --- | --- |
| `incremental difference domain` | Incremental semantic risks, interface-change risks, test gaps, and document alignment gaps caused by the currently tracked staged/unstaged diff | Does not perform system-wide CWE security checks, whole-repository static analysis review, full public impact assessment, Markdown proofreading, or formal user manual generation |
| `incremental security domain` | Security regressions, dangerous calls, boundaries, and suspicious data flow in the currently tracked staged/unstaged diff | Does not perform general logic review, test-coverage review, document alignment review, or whole-repository threat modeling |
| `factual boundary domain` | Lightweight consistency check for project facts, controlled document responsibilities, public factual boundaries, capability status, and unauthorized protected-content risk in the protected three documents | Does not perform Markdown layout proofreading, static analysis of all work units, security audit, API/ABI caller impact inference, or document body revision; does not bypass the protected-content gate for the protected three documents through fact alignment, version alignment, or factual boundary domain |
| `document quality domain` | Markdown, layout, version number, updated date, aligned-document fields, language, grammar, fact-presentation norms, conceptual conflicts, ambiguity, numbers and units, reference chains, anti-weakening gate, protected-content gate for the protected three documents, and article quality checks and allowed repairs for the six controlled documents | Does not judge correctness of code facts, does not refresh formal user manual public entry content, and does not replace factual boundary domain or documentation release domain; does not bypass the protected-content gate for the protected three documents through Markdown/format repair |
| `public impact domain` | Public entries, API usage contracts, ABI binary boundaries, caller chains, version impact inference, and coverage of the incremental semantic, interface, test-gap, and document-alignment risk slice caused by the currently tracked diff | Does not perform general code-defect static analysis review, security threat modeling, Markdown proofreading, or documentation release |
| `global security domain` | Whole-repository security threat modeling, entries/assets/trust boundaries, CWE risk matrix, and dependency security boundaries, while covering the security regression slice caused by the currently tracked diff | Does not perform general static coverage matrix, does not adjudicate API/ABI compatibility, and does not repair code or rewrite documents |
| `static analysis domain` | Static analysis coverage review covering all controlled-project-owned code reading, parseable-work-unit quality review, main logic, resource lifecycles, and cross-module relationships, while covering controlled document responsibilities, public factual boundaries, build/test entries, capability status, the unauthorized-change risk slice for protected content in the protected three documents, and minimum code-change triage within the authorized scope | Does not perform security-specific threat modeling, version impact inference, Markdown proofreading, or formal user manual generation |
| `documentation release domain` | Fully generates or broadly rewrites the formal user manual body based on public exposure and stable facts, and embeds a six-controlled-document alignment and proofreading subprocess no weaker than the corresponding capability domain of `document quality domain` | This level does not repeat the already accepted primary responsibilities of prerequisite public impact domain, global security domain, or static analysis domain; does not rerun the lightweight group's incremental difference domain; does not weaken controlled rule documents or protected content in the protected three documents through manual generation, six-document alignment proofreading, or version alignment |

### 10.6 Automatic Quality Domain Description Template and Task Split Matrix

The automatic quality guard chapter in `AGENTS.md` only retains the rule-load test, automatic quality domain list, two prefix chains, summary of `explore` / `general` or equivalent capability types, and references to Chapters 10-13 of this file. It ***must not require or copy*** the detailed structures of task briefs, subagent lifecycles, to-do plan boundaries, acceptance fields, and other per-quality-domain subsections from Chapters 11 and 12 of this file.

Only the per-quality-domain subsections in Chapters 11 and 12 of this file are authoritative detailed descriptions by domain, and they **must** describe in-group prefix chains, subagent orchestration, and acceptance hard constraints. Strong constraints must not be written only in the general principles while individual quality-domain descriptions degrade into "suggested split", "splittable", or one generalized sentence.

Each quality-domain subsection contains at least the following isomorphic elements: automatic inclusion and positioning, input scope and coverage boundary, subagent orchestration hard constraints, task split and artifacts, modification boundary and to-do plan, combination and reuse boundary. Downstream quality domains must also state the prerequisite prefix-chain levels, serial completion requirements, and stop boundary when prerequisite levels are not accepted.

Read-only checks, reviews, verifications, analyses, summaries, and rechecks in the task split matrix map by default to `explore` or a subagent type with equivalent read-only capability. Writing the to-do plan, repairing documents, aligning version numbers, updated dates, or aligned-document fields, generating section drafts, merging drafts, review modifications, and other persisted artifacts map by default to `general` or a subagent type with equivalent read/write capability. If the same matrix cell includes both read and write actions, it must be further split in the task brief.

| Quality Domain | Quality-Domain Coordinator Artifact | Execution Tasks | Summary Task | Recheck Task |
| --- | --- | --- | --- | --- |
| `incremental difference domain` | diff task brief, tracked staged/unstaged file list, uncovered untracked file list | Incremental semantic defect review, diff-related test blind-spot review, diff-related interface risk review, diff-caused document alignment gap review | Deduplicate into diff risk list and to-do plan candidates | Check whether only tracked diff was used, whether untracked content was read out of scope, and whether security-specific or whole-repository analysis was not expanded |
| `incremental security domain` | diff security task brief, CWE check domain, suspicious data-flow list | diff buffer/boundary review, dangerous function review, input-boundary review, suspicious data-flow review | Produce diff security risk list and confidence levels | Check whether general diff review was not substituted, low-confidence items are only reported and not written to the to-do plan, and evidence items have location and impact scope |
| `factual boundary domain` | factual boundary domain task brief, controlled document and project fact verification scope | Document responsibility consistency check, public entry factual boundary check, build/test entry fact check, source capability status check, protected-content unauthorized-change risk check for the protected three documents | Produce factual differences, to-do plan recording status, and next-flow recommendations | Check that Markdown proofreading, all-work-unit full analysis, manual body rewrite, security audit, or protected-content revision in the protected three documents was not performed without authorization |
| `document quality domain` | Six-document alignment verification task brief, allowed repair list, prohibited repair list, quality review list, protected-content gate list for the protected three documents | Markdown/format task, language task, concept and responsibility consistency task, numbers/units and reference chain task, anti-weakening gate task, protected-content gate task for the protected three documents, article quality task, modification and back-check task | Produce repair summary, unrepaired issues, to-do plan candidates, and remaining risks | Check that factual boundary domain or documentation release domain was not substituted, code facts or capability status were not changed, version number/updated date/aligned-document fields are consistent, Markdown/format/quality verification passed, and the protected-content gate for the protected three documents was not bypassed |
| `public impact domain` | Interface-change task brief, public exposure list, caller-chain list | API compatibility analysis, ABI compatibility analysis, interface caller-chain analysis, version-number inference | Produce public impact domain report, compatibility judgment, and document alignment recommendations | Check that API/ABI concepts were not mixed, general static analysis domain or global security domain was not substituted, and caller-chain coverage and version inference evidence are sufficient |
| `global security domain` | Whole-repository threat-modeling task brief, asset/entry/trust-boundary list, risk matrix framework | TOCTOU/injection/race/input validation/memory safety/script safety/dependency security boundary audit | Produce threat-model summary, vulnerability risk matrix, CWE mapping, and to-do plan candidates | Check risk confidence, false-positive routing, that a general static coverage matrix was not substituted, and third-party interface-level boundaries and to-do plan evidence are complete |
| `static analysis domain` | File list, parseable work-unit list, logic coverage list, cross-module relationship list, uncovered-item list, quality review list | Module/file-group/work-unit code reading, logic review, quality review, resource lifecycle review, third-party interface-level coverage, and minimal code-modification routing within the authorized scope | Produce coverage matrix, confirmed finding list, automatic repair candidates, fact alignment recommendations, and to-do plan candidates | Check that every owned parseable work unit has ownership and completed reading, security threat modeling or public impact domain was not substituted, uncovered items were not written as complete, and code modifications did not exceed authorization |
| `documentation release domain` | Public exposure list, chapter task brief, six-document alignment proofreading task brief, temporary-draft queue, acceptance conditions, protected-content gate list for the protected three documents | Chapter writing, chapter merge, chapter review, six-document alignment proofreading, quality review, protected-content gate check for the protected three documents | Produce formal manual draft, release review result, six-document revision summary, and temporary-draft handling record | Check Chapter 13 fidelity, public entry coverage, confidentiality boundary, table-of-contents jumps, example signatures, Markdown/quality checks, six-document alignment proofreading, and protected-content gate for the protected three documents, and confirm that other quality domains were not substituted |

## 11. Lightweight Review, Sensing, and Proofreading Rules

This chapter defines the four lightweight automatic quality domains: `incremental difference domain`, `incremental security domain`, `factual boundary domain`, and `document quality domain`. Lightweight automatic quality domains only inspect restricted scope or specific fact domains and do not promise whole-engineering per-work-unit coverage; however, capability detection, three-layer/two-layer architecture, prohibition on active degradation, concurrency queuing, hard-cap stop-and-resume, subagent lifecycle discipline, stop-and-report when no real subagent capability exists, and independent recheck discipline must not be relaxed.

The explicit ordered prefix chain for the lightweight automatic quality guard group is fixed as: `incremental difference domain` = `incremental difference domain`; `incremental security domain` = `incremental difference domain` -> `incremental security domain`; `factual boundary domain` = `incremental difference domain` -> `incremental security domain` -> `factual boundary domain`; `document quality domain` = `incremental difference domain` -> `incremental security domain` -> `factual boundary domain` -> `document quality domain`. Chain levels must complete serially. Each level has an independent task brief, subagent orchestration, report, acceptance, and to-do plan candidate boundary. If a prerequisite level fails, blocks, is interrupted by a hard cap, or needs user adjudication, downstream levels must not start.

### 11.1 incremental difference domain

#### 11.1.1 Automatic Inclusion and Positioning

When the risk, impact surface, or user request of an ordinary task causes `incremental difference domain` to be automatically included in lightweight automatic quality guard mode, execute the first level of the lightweight chain. This domain only analyzes the staged/unstaged Git diff scope of currently tracked files and focuses on incremental change risks. Untracked files are not read for content and no equivalent diff is generated; they are only listed in the coverage summary as uncovered scope or recommended for separate inclusion.

This domain does not perform system security/CWE checks, whole-engineering static analysis review, full public impact assessment, Markdown proofreading, or formal user manual generation. When suspected security issues are found, record them only as diff risks and recommend automatic inclusion of `incremental security domain` as needed. Unless the issue already has clear evidence, impact scope, and recommended action inside the diff, it must not be written to the to-do plan.

#### 11.1.2 Input Scope and Check Focus

- Incremental defects: obvious logic errors, missing boundary conditions, resource lifecycle changes, hot-path violations, and missing exception paths.
- Document alignment gaps: public entries, API/interfaces, build scripts, test entries, capability status, or controlled facts changed without corresponding document updates.
- Test coverage blind spots: new behavior, boundaries, or interface changes have no corresponding tests or verification path.
- Interface change risks: impact on public declarations, export macros, structure layouts, enums, function pointers, calling conventions, `{{%PRIMARY_LANGUAGE}}` public semantics, and installation artifacts.
- Borrowing-semantic regressions: whether newly added or modified code removes `const` / readonly constraints, expands mutable state, changes input/output direction, changes no-alias / overlap contracts, introduces shared mutable aliases, or misses corresponding tests and public explanations.

#### 11.1.3 Subagent Orchestration Hard Constraints

Capability detection must be completed before execution. When nested subagents are supported, use a three-layer architecture of session agent, incremental difference domain coordinator, and incremental semantics/interface risk/test blind spot/document gap/recheck tasks. When only the session agent has splitting capability, use a two-layer sibling architecture. As long as any subagent splitting capability exists, execution must not actively degrade to a single agent. When concurrency is insufficient, queue according to the task brief. When the hard cap is exhausted, stop for continuation. When no real subagent capability exists at all, ***stop and report***, preserving task brief, uncovered items, and recovery entry. Read-only tasks in this domain, such as coordination, review, summary, and recheck, use `explore` or a subagent type with equivalent read-only capability. If confirmed issues need to be written to `agents/TODO.md`, a separate `general` or equivalent read/write subagent type must perform the write. The parent agent must not privately end incomplete subagents because they run long, temporarily produce no output, progress slowly, or wait in queue.

#### 11.1.4 Task Split and Artifacts

The coordinator establishes the tracked staged/unstaged diff file list, uncovered untracked file list, review task brief, and acceptance conditions. Execution tasks are separately responsible for incremental semantic defects, interface risks, test blind spots, and document alignment gaps. The summary task outputs diff coverage summary, finding list, interface change risks, document alignment gaps, test coverage blind spots, and remaining risks. The recheck task confirms that untracked content was not read out of scope and that security-specific or whole-repository analysis was not substituted.

#### 11.1.5 Modification Boundary, To-Do Plan, and Reuse

This domain does not modify code. Confirmed issues with evidence location, impact scope, and recommended action that need later handling are automatically submitted to `agents/TODO.md`. The same-round Git diff file list may be reused. Conclusions from global security domain, static analysis domain, public impact domain, or document quality domain must not be reused. When this level is automatically covered as a prerequisite in a downstream prefix chain, this level's report and to-do plan boundary still require independent acceptance; downstream levels may start only after acceptance passes.

### 11.2 incremental security domain

#### 11.2.1 Automatic Inclusion and Positioning

When the risk, impact surface, or user request of an ordinary task causes `incremental security domain` to be automatically included in lightweight automatic quality guard mode, execute the second level of the lightweight chain; `incremental difference domain` must first be completed and accepted. This domain scans only security regressions, dangerous calls, boundary issues, and suspicious data flow inside the currently tracked staged/unstaged diff scope, focusing on incremental security risks.

This domain does not perform general logic review, test coverage review, document alignment review, whole-repository threat modeling, or API/ABI impact inference. It does not replace the prerequisite `incremental difference domain` diff risk report, and does not replace `global security domain` or `public impact domain`.

#### 11.2.2 Input Scope and Check Focus

- Buffer boundaries, length calculations, integer overflow, null pointers, lifecycles, use-after-free, and out-of-bounds access.
- Dangerous functions, format strings, file path handling, input boundaries, unvalidated external input, and suspicious data flow.
- Security regressions related to `{{%PRIMARY_LANGUAGE_OR_RUNTIME}}` ABI, public structures, handle lifecycles, and hot-path state management.
- Borrowing-semantics security regressions such as incorrect `restrict` / no-alias assumptions, overlapping-buffer out-of-bounds access, shared mutable state races, lifecycle escapes, writes to readonly objects, or bypassed unique mutable entries.

#### 11.2.3 Subagent Orchestration Hard Constraints

Capability detection must be completed before execution. When nested subagents are supported, use a three-layer architecture of session agent, incremental security domain coordinator, and boundary review/dangerous call review/input boundary review/suspicious data-flow review/recheck tasks. When only the session agent has splitting capability, use a two-layer sibling architecture. As long as any subagent splitting capability exists, active degradation is prohibited. When concurrency is insufficient, queue. When the hard cap is exhausted, stop for continuation. When no real subagent capability exists at all, ***stop and report***, preserving task brief, uncovered items, and recovery entry. Read-only tasks such as security review, data-flow check, summary, and recheck in this domain use `explore` or a subagent type with equivalent read-only capability. If high-confidence confirmed issues need to be written to `agents/TODO.md`, a separate `general` or equivalent read/write subagent type must perform the write. The parent agent must not privately end incomplete subagents because they run long, temporarily produce no output, progress slowly, or wait in queue.

#### 11.2.4 Task Split and Artifacts

The coordinator establishes the diff security task brief, CWE check domain, and suspicious data-flow list. Execution tasks cover buffer/boundary, dangerous functions, input boundaries, and suspicious data flow. The summary task outputs the diff security risk list, CWE categories, evidence locations, impact scope, confidence, and recommended first action. The recheck task confirms that general diff review was not substituted, low-confidence items are reported only, and evidence items have location and impact scope.

#### 11.2.5 Modification Boundary, To-Do Plan, and Reuse

This domain does not modify code. Only high-confidence confirmed issues with evidence location, impact scope, and recommended action are automatically submitted to `agents/TODO.md`; low-confidence or tool-uncertain items remain in the report. Same-round or prerequisite Git diff file lists may be reused, but general incremental difference domain conclusions or whole-repository global security audit conclusions must not be reused. Lightweight-chain downstream levels or cross-group `global security domain` must not be started out of order.

### 11.3 factual boundary domain

#### 11.3.1 Automatic Inclusion and Positioning

When the risk, impact surface, or user request of an ordinary task causes `factual boundary domain` to be automatically included in lightweight automatic quality guard mode, execute the third level of the lightweight chain; `incremental difference domain` and `incremental security domain` must first be completed and accepted serially. This domain lightly checks project facts, controlled document responsibilities, public factual boundaries, build/test entries, capability status, and unauthorized protected-content risk in the protected three documents to find obvious factual inconsistency, responsibility-boundary drift, public entry fact gaps, inaccurate build/test entry descriptions, mislabeled source capability status, and suspected bypass of protected content in the protected three documents.

This domain does not perform Markdown layout proofreading, link proofreading, table proofreading, code fence repair, static analysis of all work units, security audit, API/ABI caller impact inference, incremental difference domain, formal manual body revision, or protected-content revision in the protected three documents. When the formal user manual body needs systematic refresh based on code facts, only report and recommend running `documentation release domain`. When protected content in the protected three documents needs modification, the current task must stop and follow the project-constraint document hard write gate in Chapter 10.

#### 11.3.2 Input Scope and Minimum Fact Domains

- Whether controlled document versions, responsibilities, cross-reference consistency, and protected content in the protected three documents have unauthorized changes.
- Obvious factual boundaries of genuinely applicable public entries among APIs, CLIs, SDKs, services, plugins, protocols, configurations, user interfaces, data formats, model entries, deployment entries, operations entries, documentation entries, public headers where applicable, public schemas, protocol documents, configuration descriptions, types, enums, structures, or language-level public semantics.
- Description consistency of build entries, installation entries, test entries, and script entries.
- Source capability status, placeholder modules, skeleton modules, and published capability status.
- Obvious responsibility-boundary and capability-status conflicts between the formal manual and public facts. Manual Markdown syntax, table-of-contents links, tables, code blocks, blank lines, rendering continuity, and layout anomalies are not handled in factual boundary domain and should recommend automatic inclusion of `document quality domain`.

#### 11.3.3 Subagent Orchestration Hard Constraints

Capability detection must be completed before execution. When nested subagents are supported, use a three-layer architecture of session agent, factual boundary domain coordinator, and document responsibility/public entry/build-test entry/source capability status/protected-content gate for protected three documents/recheck tasks. When only the session agent has splitting capability, use a two-layer sibling architecture. As long as any subagent splitting capability exists, active degradation is prohibited. When concurrency is insufficient, queue. When the hard cap is exhausted, stop for continuation. When no real subagent capability exists at all, ***stop and report***, preserving task brief, uncovered fact domains, and recovery entry. Read-only tasks such as fact verification, capability status verification, protected-content gate check for the protected three documents, summary, and recheck use `explore` or a subagent type with equivalent read-only capability. If confirmed issues need to be written to `agents/TODO.md` or necessary version number, updated date, or aligned-document fields need alignment, a separate `general` or equivalent read/write subagent type must perform the write. Any protected-content modification in the protected three documents beyond the narrow version-metadata exception must stop the current task and request confirmation. The parent agent must not privately end incomplete subagents because they run long, temporarily produce no output, progress slowly, or wait in queue.

#### 11.3.4 Task Split and Artifacts

The coordinator establishes the factual boundary domain task brief, controlled documents, project fact verification scope, and protected-content gate list for the protected three documents. Execution tasks are separately responsible for document responsibility consistency, public entry factual boundaries, build/test entry facts, source capability status, and unauthorized protected-content risk in the protected three documents. The summary task outputs factual boundary domain task brief summary, completed factual boundary domain, incomplete factual boundary domain, discovered factual differences, to-do plan write status, reasons not revised, and recommended next handling. The recheck task confirms that Markdown proofreading, all-work-unit full analysis, manual body rewrite, security audit, or protected-content revision in the protected three documents was not performed without authorization.

#### 11.3.5 Modification Boundary, To-Do Plan, and Reuse

Except for confirmed issue writing to `agents/TODO.md` and necessary version number, updated date, and aligned-document field alignment triggered by it, this domain does not directly revise body text of `README.md`, `AGENTS.md`, `agents/RULES.md`, `agents/BASE.md`, `doc/DOCUMENTATION.md`, or the formal manual body. Necessary version alignment must not be used to revise protected content in the protected three documents. To-do items, factual gaps, and known issues with evidence location, impact scope, and recommended action are automatically submitted to `agents/TODO.md`. Same-round read-only public exposure lists, controlled document lists, build-entry lists, or prerequisite file lists may be reused. Conclusions from document quality domain, static analysis domain, global security domain, or public impact domain must not be reused.

### 11.4 document quality domain

#### 11.4.1 Automatic Inclusion and Positioning

When the risk, impact surface, or user request of an ordinary task causes `document quality domain` to be automatically included in lightweight automatic quality guard mode, execute the fourth level of the lightweight chain; `incremental difference domain`, `incremental security domain`, and `factual boundary domain` must first be completed and accepted serially.

This domain checks and, within the allowed scope, repairs Markdown syntax, structural disorder, layout, version number, updated date, aligned-document fields, language, grammar, fact-presentation norms, conceptual consistency, ambiguity, numbers and units, reference chains, anti-weakening gates, protected-content gates for the protected three documents, and article quality across the six controlled documents. This domain does not judge whether code facts, public entry facts, or capability status are correct. When suspected factual conflicts are found, they are reported only as prohibited repair items and handled according to the to-do plan boundary; body text is not corrected in place.

#### 11.4.2 Allowed Scope and Prohibited Scope

The allowed scope includes Markdown syntax, layout, heading hierarchy, table-of-contents links, misaligned table columns, code fences, list indentation, blank lines, trailing whitespace, line ending and encoding format (for example CRLF/BOM, LF/UTF-8 with BOM, or an equivalent project-declared policy), EOF newline, version number, updated date, and aligned-document fields in `README.md`, `AGENTS.md`, `agents/RULES.md`, `agents/BASE.md`, `agents/TODO.md`, and `doc/DOCUMENTATION.md`. Even when protected content in the protected three documents has Markdown/format, language, or version-description problems, it must first be judged whether it only belongs to the narrow version-metadata exception. If it exceeds the narrow exception, the current task must stop and the project-constraint document hard write gate in Chapter 10 must be executed.

Language proofreading is allowed, including typo, missing word, extra word, repeated word, awkward sentence, punctuation, terminology inconsistency, syntax/grammar errors, and unsmooth technical documentation expression. Problems in fact presentation that is non-standard, unclear, incompletely referenced, ambiguous in pronoun reference, vague in concept boundary, unclear in rule subject, unclear in condition exception, or unclear in responsibility chain may be revised only when facts, meaning, constraint strength, and behavior boundaries do not change.

API/ABI concept mixing, document responsibility boundary conflicts, automatic quality guard boundary ambiguity, version-alignment description ambiguity, and inconsistent to-do plan recording standards that can already be judged inside the six controlled documents may be revised. Problems that can be directly judged from the responsibility priority of the six controlled documents, current stable facts, and clear rules may be revised in place. However, protected content in the protected three documents must not be revised directly through proofreading; the project-constraint document hard write gate must be executed. Problems requiring deep source judgment, public API fact adjudication, capability status updates, systematic formal user manual public entry refresh, or new design decisions are only reported or handled according to the to-do plan boundary.

Number and unit consistency checks are based only on the six controlled documents and cover version numbers, dates, chapter numbers, quantities, ranges, priorities, path counts, command counts, time, samples, bytes, elements, seconds, Hz, dB, radians, normalized frequency, interval openness/closedness, casing, spaces, and parameter unit expressions. Number and unit issues that require source code, public API, or implementation facts for adjudication must not be guessed and revised; they are only reported or entered as to-do plan candidates.

Reference chain integrity checks cover only internal references, section anchors, version chains, file paths, responsibility chains, to-do plan evidence, source quality domains, public fact entries, and formal manual public fact entries inside the six controlled documents. They require traceability, no broken chains, no circular misdirection, and no reverse definition of project facts. They do not extend to external materials, network materials, or source fact adjudication.

Anti-weakening gate checks must confirm that strong constraint terms and prohibition boundaries are preserved or strengthened, and prohibit weakening "must", "must not", "can only", or "stop and report". When Chapter 13 is involved, chapter responsibilities, templates, QA checklists, confidentiality boundaries, public exposure coverage, source awareness, example signature checks, and old-subsection mapping requirements must be preserved or strengthened. When protected content in the protected three documents is involved, it must be confirmed that Markdown/format repair, ordinary version alignment, or six-document alignment verification did not bypass the Chapter 10 hard gate.

Article quality checks cover heading and table-of-contents consistency, paragraph focus, logical order, causal relationships, conditions and exceptions, negative scope, parallel item granularity, list numbering, table fields, code identifiers, file paths, command names, casing, parentheses, quotation marks, first definition of terms, redundant repetition, tense consistency, reader perspective, and confidentiality boundaries.

It is prohibited to change code facts, public entry facts, API/interface facts, capability status, to-do plan semantics, formal user manual public entry descriptions, example semantics, parameter explanations, capability boundaries, or protected content in the protected three documents. It is prohibited to expand document quality domain into code fact review, factual boundary domain, documentation release domain, public entry fact refresh, source capability status redetermination, systematic formal manual rewrite, code repair, or project constraint document rewrite.

#### 11.4.3 Subagent Orchestration Hard Constraints

Capability detection must be completed before execution. When nested subagents are supported, use a three-layer architecture of session agent, document quality domain coordinator, Markdown/format task, language task, concept and responsibility consistency task, numbers/units and reference chain task, anti-weakening gate task, protected-content gate task for the protected three documents, article quality task, modification and back-check task, and independent recheck task. When only the session agent has splitting capability, use a two-layer sibling architecture. As long as any subagent splitting capability exists, active degradation is prohibited. When concurrency is insufficient, queue. When the hard cap is exhausted, stop for continuation. When no real subagent capability exists at all, ***stop and report***, preserving task brief, uncovered check domains, and recovery entry. Read-only checks such as Markdown/format, language, concept responsibilities, numbers/units/reference chains, anti-weakening, protected-content gates for the protected three documents, article quality, and independent recheck use `explore` or a subagent type with equivalent read-only capability. In modification and back-check tasks, any step involving writing the six controlled documents, version number, updated date, aligned-document fields, or to-do plan uses `general` or a subagent type with equivalent read/write capability; pure read-only back-checks may be split into `explore` or equivalent read-only tasks. Writes involving protected content in the protected three documents must first satisfy the Chapter 10 hard gate. The parent agent must not privately end incomplete subagents because they run long, temporarily produce no output, progress slowly, or wait in queue.

#### 11.4.4 Task Split and Artifacts

The coordinator establishes the six-document alignment verification task brief, allowed repair list, prohibited repair list, terminology list, concept conflict list, number and unit list, reference chain list, anti-weakening gate list, protected-content gate list for the protected three documents, and article quality list. Quality check tasks read-only check the six controlled documents and output issue lists, file line numbers, issue types, allowed repair judgments, and prohibited repair judgments. Modification and back-check tasks handle only allowed repairs; after completion, they rerun Markdown/lint/format/version consistency, terminology, numbers and units, reference chains, anti-weakening gates, and protected-content gate checks for the protected three documents. The recheck task confirms that code facts, public entry facts, API/interface facts, capability status, formal manual public entry facts, protected content in the protected three documents, and to-do plan semantics were not changed; factual boundary domain or documentation release domain was not substituted; version number, updated date, and aligned-document fields are consistent; and Markdown/format/quality verification passed.

#### 11.4.5 Modification Boundary, To-Do Plan, and Reuse

This domain may modify the six controlled documents within the allowed scope, but protected content in the protected three documents can only be aligned inside the narrow version-metadata exception. Anything beyond the narrow exception must stop the current task and execute the project-constraint document hard write gate. Confirmed issues judged to be code facts, public entry facts, API/interface facts, source capability status, safety, compatibility, or formal manual systematic refresh problems that cannot be repaired in document quality domain are automatically submitted to `agents/TODO.md`. Same-round controlled document file lists, version lists, internal reference lists, Markdown checklists, or prerequisite read-only lists may be reused. factual boundary domain fact conclusions must not be reused to directly correct body text, and `documentation release domain` must not be started cross-group. Proofreading of `doc/DOCUMENTATION.md` remains bounded by formal user manual perspective: language, concept, and clear-conflict corrections are allowed; bulk refresh of public entries, example semantics, or parameter facts under the name of proofreading is not allowed.

## 12. Full Automatic Quality-Control Group: public impact domain, global security domain, static analysis domain, and documentation release domain Rules

This chapter defines the four full automatic quality domains: `public impact domain`, `global security domain`, `static analysis domain`, and `documentation release domain`. Full automatic quality domains need to establish public exposure, caller chains, threat models, coverage matrices, or formal manual artifacts; however, quality-domain bodies must remain low coupling, and the primary responsibility of one chain level must not be merged into another chain level. Full automatic quality domains must strictly include the corresponding lightweight automatic quality domains in capability. This inclusion relationship is reflected only through the full chain level's own task brief, check items, report, and acceptance; it ***must not*** be rewritten as rerunning lightweight quality domains or reusing lightweight quality-domain conclusions to replace the full chain level's primary responsibilities.

The explicit ordered prefix chain for the full automatic quality guard group is fixed as: `public impact domain` = `public impact domain`; `global security domain` = `public impact domain` -> `global security domain`; `static analysis domain` = `public impact domain` -> `global security domain` -> `static analysis domain`; `documentation release domain` = `public impact domain` -> `global security domain` -> `static analysis domain` -> `documentation release domain`. Chain levels must complete serially. Each level has an independent task brief, subagent orchestration, report, acceptance, and to-do plan candidate boundary. If a prerequisite level fails, blocks, is interrupted by a hard cap, or needs user adjudication, downstream levels must not start.

### 12.1 public impact domain

#### 12.1.1 Automatic Inclusion and Positioning

When the risk, impact surface, or user request of an ordinary task causes `public impact domain` to be automatically included in full automatic quality guard mode, execute the first level of the full chain. This domain establishes the public exposure list, API usage contracts, ABI binary boundaries, caller chains, installation or release artifacts, and version impact inference, and outputs compatibility judgments, document alignment recommendations, and remaining risks.

This domain does not perform general code-defect static analysis review, security threat modeling, Markdown proofreading, or documentation release. It does not replace or rerun `incremental difference domain`, `static analysis domain`, `global security domain`, or `documentation release domain`; however, the incremental risk capability domain of `incremental difference domain` must be embedded in this level's task brief and acceptance.

#### 12.1.2 Input Scope and Coverage Boundary

- Public exposure list, including APIs, CLIs, SDKs, services, plugins, protocols, configurations, user interfaces, data formats, model entries, deployment entries, operations entries, documentation entries, and other user-visible usage contracts.
- The binary ABI branch is enabled only when the project has exported symbols, calling conventions, public structure layouts, enum underlying types, function pointers, opaque handles, `{{%EXTERNAL_LINKAGE_MODEL}}` function families, link artifacts, or binary compatibility promises. If not applicable, "not applicable" must be marked; public headers where applicable or ABI must not be fabricated.
- Caller chains and fact dependencies of `{{%SOURCE_OR_CONTENT_ROOT}}`, `{{%RUN_TEST_DEMO_GENERATE_MAINTENANCE_ENTRY_PATH_OR_IDENTIFIER}}`, build scripts, installation or release artifacts, test entries, deployment entries, and public documents on public entry changes.
- Public entry, API, ABI, capability status, build/installation, release artifact, and test entry facts in the six controlled documents.
- Read-only / writable / input-output, ownership, lifecycles, shared readonly, unique mutable, no-alias, and buffer-overlap contracts in public entries, and the impact of changes to these contracts on callers, ABI/binding layers, tests, and the user manual.
- If currently tracked staged/unstaged diff exists, this level must cover incremental semantic risks, interface change risks, test gaps, and document alignment gaps caused by the diff as a public impact slice. This slice is not equivalent to separately running `incremental difference domain`.

#### 12.1.3 Subagent Orchestration Hard Constraints

Capability detection must be completed before execution. When nested subagents are supported, use a three-layer architecture of session agent, public impact domain coordinator, and public entry/API compatibility/ABI compatibility/caller-chain/version inference/recheck tasks. When only the session agent has splitting capability, use a two-layer sibling architecture. As long as any subagent splitting capability exists, active degradation is prohibited. When concurrency is insufficient, queue. When the hard cap is exhausted, stop for continuation. When no real subagent capability exists at all, ***stop and report***, preserving task brief, uncovered items, and recovery entry. Read-only tasks such as public entry analysis, interface analysis, caller-chain analysis, version inference, summary, and recheck in this domain use `explore` or a subagent type with equivalent read-only capability. If confirmed issues need to be written to `agents/TODO.md`, a separate `general` or equivalent read/write subagent type must perform the write. The parent agent must not privately end incomplete subagents because they run long, temporarily produce no output, progress slowly, or wait in queue.

#### 12.1.4 Task Split and Artifacts

The coordinator establishes the public entry change task brief, public exposure list, caller-chain list, and version-inference acceptance conditions. Execution tasks are separately responsible for public entry compatibility analysis, API compatibility analysis, ABI compatibility analysis, caller-chain analysis, and version number inference. The summary task forms the public impact domain report, compatibility judgment, and document alignment recommendations. The recheck task confirms that public entry, API, and ABI concepts are not mixed, general static analysis domain or global security domain was not substituted, and caller-chain coverage and version-inference evidence are sufficient.

#### 12.1.5 Modification Boundary, To-Do Plan, and Reuse

This domain does not modify code. Confirmed issues with evidence location, impact scope, and recommended action that need later handling are automatically submitted to `agents/TODO.md`. Same-round public exposure lists or diff file lists may be reused, but conclusions from incremental difference domain, static analysis domain, global security domain, or documentation release domain must not be reused. When this level is automatically covered as a prerequisite in a downstream prefix chain, this level's report and to-do plan boundary still require independent acceptance; downstream levels may start only after acceptance passes.

### 12.2 global security domain

#### 12.2.1 Automatic Inclusion and Positioning

When the risk, impact surface, or user request of an ordinary task causes `global security domain` to be automatically included in full automatic quality guard mode, execute the second level of the full chain; `public impact domain` must first be completed and accepted. This domain performs whole-repository threat modeling, entry/asset/trust boundary analysis, CWE risk matrix, and dependency security boundary audit.

This domain does not perform general static coverage matrices, API/ABI compatibility adjudication, version-number inference, Markdown proofreading, or formal user manual generation, and does not replace or rerun diff-only `incremental security domain`; however, the incremental security capability domain of `incremental security domain` must be embedded in this level's task brief and acceptance.

#### 12.2.2 Input Scope and Check Focus

- TOCTOU, injection, race conditions, unvalidated input, path handling, dangerous functions, buffers, integer overflow, use-after-free, double-free, uninitialized reads, and suspicious data flow.
- If currently tracked staged/unstaged diff exists, this level must cover diff security regressions, dangerous calls, boundary issues, and suspicious data flow as an incremental security slice inside whole-repository global security. This slice is not equivalent to separately running `incremental security domain`.
- Public entry boundaries, API usage contracts, service or protocol boundaries, configuration and data-format boundaries, `{{%PRIMARY_LANGUAGE_OR_RUNTIME}}` ABI boundaries, resource lifecycles, handle or session lifecycles, parallel tasks, file IO, logs, `{{%FILE_IO_CAPABILITY_DOMAIN}}` processing, build scripts, deployment entries, and test entries.
- Forced closing of handles, pointers, objects, locks, processes, IPC resources, or equivalent external resource release operations in automation build scripts, build cleanup scripts, CI workflows, and task-entry call chains.
- Shared readonly and unique mutable boundaries, readonly inputs, unique outputs, no-alias / overlap contracts, `restrict` or equivalent alias restrictions, lifetime escape, shared mutable aliases, and cross-thread sharing semantics.
- Third-party, externally maintained, or independent dependencies are covered at interface-level security boundaries, focusing on this project's call boundaries, configuration macros, memory/alignment assumptions, and error propagation.

#### 12.2.3 Subagent Orchestration Hard Constraints

Capability detection must be completed before execution. When nested subagents are supported, use a three-layer architecture of session agent, global security domain coordinator, and entry/assets/memory safety/concurrency and TOCTOU/scripts and paths/dependency boundary/recheck tasks. When only the session agent has splitting capability, use a two-layer sibling architecture. As long as any subagent splitting capability exists, active degradation is prohibited. When concurrency is insufficient, queue. When the hard cap is exhausted, stop for continuation. When no real subagent capability exists at all, ***stop and report***, preserving task brief, uncovered items, and recovery entry. Read-only tasks such as threat modeling, entries/assets, memory safety, concurrency, scripts/paths, dependency boundaries, summary, and recheck in this domain use `explore` or a subagent type with equivalent read-only capability. If confirmed issues need to be written to `agents/TODO.md`, a separate `general` or equivalent read/write subagent type must perform the write. The parent agent must not privately end incomplete subagents because they run long, temporarily produce no output, progress slowly, or wait in queue.

#### 12.2.4 Task Split and Artifacts

The coordinator establishes the whole-repository threat modeling task brief, asset/entry/trust boundary list, and risk matrix framework. Execution tasks cover TOCTOU, injection, race, input validation, memory safety, script safety, and dependency security boundaries. The summary task outputs threat-model summary, vulnerability risk matrix, CWE mapping, impact scope, evidence location, confidence, recommended first action, verification recommendation, and remaining risks. The recheck task confirms risk confidence, false-positive routing, that a general static coverage matrix was not substituted, third-party interface-level boundaries, and to-do plan evidence completeness.

#### 12.2.5 Modification Boundary, To-Do Plan, and Reuse

This domain does not modify code. Confirmed issues with evidence location, impact scope, and recommended action that need later handling are automatically submitted to `agents/TODO.md`; low-confidence items are only reported. Same-round file lists, public entry lists, dependency lists, or prerequisite public impact domain read-only lists may be reused. The diff conclusions of `incremental security domain` must not be reused as whole-repository conclusions, and prerequisite compatibility conclusions must not be reused to replace this level's security conclusions. Full-chain downstream levels must not be started out of order.

### 12.3 static analysis domain

#### 12.3.1 Automatic Inclusion and Positioning

When the risk, impact surface, or user request of an ordinary task causes `static analysis domain` to be automatically included in full automatic quality guard mode, execute the third level of the full chain; `public impact domain` and `global security domain` must first be completed and accepted serially. This domain establishes a coverage matrix for all owned code, test code, scripts, build entries, configuration parsing entries, documentation release entries, public-entry-related implementations, data flows, declaration units, routes, tasks, jobs, rules, or other real parseable work units in the controlled project, performs code reading and quality review, finds risks, confirms errors, identifies factual gaps, and handles them according to the automatic repair routing rules. Issues that can be safely repaired within the current authorized scope must receive the minimal necessary code modification; out-of-scope, high-risk, insufficient-evidence, unverifiable, or user-adjudication issues are recorded in `agents/TODO.md` or reported as adjudication items.

This domain is the full-group prerequisite chain level for `documentation release domain`, but this level's primary responsibility must not be merged into `documentation release domain`. This level does not perform security-specific threat modeling, API/ABI version impact inference, Markdown proofreading, or formal user manual generation, and does not replace or rerun `factual boundary domain`; however, the factual boundary, responsibility consistency, capability status, and protected-three-documents unauthorized-change risk capability domain of `factual boundary domain` must be embedded in this level's task brief and acceptance.

#### 12.3.2 Input Scope and Coverage Gate

`static analysis domain` must first establish file lists, parseable work-unit lists, logic coverage lists, cross-module relationship lists, uncovered item lists, quality review lists, and remaining queues. All owned code, test code, scripts, build entries, configuration parsing entries, documentation release entries, public-entry-related implementations, data flows, declaration units, routes, tasks, jobs, rules, or other real parseable work units in the controlled project must have analysis ownership and complete actual source reading. In code projects, functions, template functions, class methods, exported wrappers, test entries, script entries, route handlers, configuration parsing entries, and generation entries are required work units. Non-code projects replace them with document paragraphs, data tables, configuration items, process nodes, pages, task rules, or other real parseable units. Automation build scripts, build configurations, CI workflows, and task-orchestration entry call chains are build-entry-related parseable work units and must be included in the coverage list by relative path or task locator. Uncovered work units must not be hidden through merged tasks, generic descriptions, read-only file names, symbol indexes, or by looking only at public declarations. Source-integrated third-party libraries, vendor content, submodules, derived dependencies, generated artifacts, caches, and unparseable binaries are not included in equivalent per-work-unit deep reading; unless the user explicitly requests otherwise, handle them only as third-party interface-level boundaries, caller-side risks, exclusions, or uncovered items.

When establishing file lists, parseable work-unit lists, call relationships, or cross-module relationship lists, if the current environment has code indexes, symbol navigation, reference lookup, call graphs, or semantic retrieval capabilities, they must be used first to assist in locating work units, public-entry references, caller chains, and uncovered items. Index results may enter the coverage matrix only after source reading or public-entry fact recheck. If indexes are unavailable, stale, insufficient in coverage, or conflict with source facts, index status must be recorded and the process must fall back to file search, content search, and source reading; unknown scope caused by missing indexes ***must not*** be written as covered.

Logic coverage means static review covers main branches, state advancement, resource lifecycles, error boundaries, data ownership, shared readonly access, unique mutable access, readonly inputs, unique outputs, alias or reference relationships, no-alias / overlap contracts, hot-path constraints, `{{%DATA_PARALLEL_ACCELERATION_BACKEND}}` fallback, preparation-phase and processing-phase responsibilities, cross-module relationships, public entries, API/ABI, or usage-contract observable boundaries inside work units. Quality review must also cover maintainability, duplicate logic, boundary conditions, error-handling paths, test blind spots, minimal code modification candidates, verification entries, and rollback boundaries. This requirement does not promise formal proof, runtime exhaustive path proof, or test coverage rate.

Third-party, externally maintained, or independent dependencies under `{{%THIRD_PARTY_DEPENDENCY_DIRECTORY}}/` are covered at interface level, focusing on this project's call boundaries, configuration macros, export impact, compile gates, memory/alignment assumptions, error propagation, and risks. Without a clear requirement, they need not be deeply read per work unit to the same degree as owned project content, and dependency source must not be modified without authorization.

This level's static coverage must also include a read-only consistency slice for project facts, controlled document responsibilities, public factual boundaries, build/test entries, capability status, and unauthorized protected-content risk in the protected three documents. This slice is not equivalent to separately running `factual boundary domain`, and protected documents must not be revised without authorization.

#### 12.3.3 Subagent Orchestration Hard Constraints

Capability detection must be completed before execution. When nested subagents are supported, use a three-layer architecture of session agent, static analysis domain coordinator, module/file-group/work-unit execution tasks, summary tasks, and recheck tasks. When only the session agent has splitting capability, use a two-layer sibling architecture. As long as any subagent splitting capability exists, active degradation is prohibited. When concurrency is insufficient, queue and ***must not reduce task count***. When the hard cap is exhausted, stop and preserve the task brief, coverage matrix, and remaining queue. When no real subagent capability exists at all, ***stop and report*** and ***do not switch to a single agent*** to execute this domain's primary task in phases. Read-only tasks such as file lists, work-unit lists, code reading, logic review, quality review, relationship review, summary, and recheck in this domain use `explore` or a subagent type with equivalent read-only capability. If confirmed issues need to be written to `agents/TODO.md`, or if confirmed issues within the current authorized scope need minimal code modification, verification, and back-check, a separate `general` or equivalent read/write subagent type must perform the write. Code modification tasks must start only after read-only review summary, read/write ownership confirmation, and modification-boundary confirmation, and must not run in parallel with read-only recheck or other write tasks for the same file. The parent agent must not privately end incomplete subagents because they run long, temporarily produce no output, progress slowly, or wait in queue.

#### 12.3.4 Task Split and Artifacts

The coordinator establishes file lists, parseable work-unit lists, logic coverage lists, cross-module relationship lists, quality review lists, and uncovered item lists. Execution tasks are split at fine granularity by module, file group, work unit, or logic domain; split granularity must be sufficient to track each file and work unit's ownership, reading status, quality review conclusion, and modification candidates. Code projects must be split down to functions, template functions, class methods, exported wrappers, test entries, script entries, or equivalent parseable code units. Non-code projects must be split down to real parseable document, data, process, page, or rule units. The summary task forms the coverage matrix, confirmed finding list, automatic repair candidates, user adjudication items, to-do plan candidates, and fact alignment recommendations. The recheck task confirms that every owned parseable work unit has ownership and completed reading, security threat modeling or public impact domain was not substituted, uncovered items were not written as complete, automatic repair candidates did not exceed authorization, and modified code completed targeted verification and back-check.

#### 12.3.5 Modification Boundary, To-Do Plan, and Reuse

This domain must not modify rule documents, protected content in the protected three documents, public-entry contracts, build scripts, or test entries by default. When the current user task has authorized source-code modification and the confirmed issue belongs to controlled-project owned code, has clear scope, sufficient evidence, local impact, reversibility, verifiability, and does not trigger public-contract or high-risk boundaries, the minimal necessary code modification, targeted verification, and back-check must be performed according to the automatic repair routing rules. Unauthorized repairs, out-of-scope issues, high-risk issues, public-contract-impacting issues, rule-document-related issues, insufficient-evidence issues, unverifiable issues, or issues needing user adjudication should enter `agents/TODO.md` or be reported as user adjudication items. Unverified guesses, generic risks, tool false positives, and complete per-work-unit logs should not be mechanically written into the controlled to-do plan. Same-round file lists, public exposure lists, or prerequisite read-only lists may be reused, but conclusions from `global security domain`, `public impact domain`, or `documentation release domain` must not be reused to replace this level's coverage matrix, logic review, quality review, repair routing, or recheck.

`static analysis domain` output contains at least: capability detection result, task brief summary, all-owned-code reading coverage conclusion, file coverage matrix, work-unit coverage matrix, main logic coverage summary, code quality review summary, cross-module relationship summary, third-party dependency interface-level coverage summary, confirmed finding list, automatic repair / to-do plan / user adjudication routing result, minimal modification list within the authorized scope, verification result, unrepaired-item reasons, uncovered items, and remaining risks.

### 12.4 documentation release domain

#### 12.4.1 Automatic Inclusion and Positioning

When the risk, impact surface, or user request of an ordinary task causes `documentation release domain` to be automatically included in full automatic quality guard mode, execute the fourth level of the full chain; `public impact domain`, `global security domain`, and `static analysis domain` must first be completed and accepted serially. This domain executes the manual generation quality-domain process according to this chapter and fully generates or broadly rewrites the body of `doc/DOCUMENTATION.md` according to Chapter 13, Formal User Manual Writing Rules.

The "documentation release" in this domain only refers to generation, merging, review, and quality acceptance before the `doc/DOCUMENTATION.md` formal user manual body enters controlled release state, and ***must not*** be interpreted as external repository publishing, version release, directory synchronization, public release process, Git operations, or release authorization for all six controlled documents.

The internal project-state precheck in this domain only serves manual fact calibration and is not equivalent to the primary responsibility of lightweight-group `factual boundary domain`. This level does not repeat the already accepted primary responsibilities of prerequisite public impact domain, global security domain, or static analysis domain, and does not rerun the lightweight group's incremental difference domain. Prerequisite reports can only be used as accepted input sources and must not replace this level's manual generation task brief, chapter writing, chapter merge, chapter review, six-document alignment proofreading, final release review, protected-content gate for the protected three documents, or to-do plan boundary. When consuming prerequisite read-only results, the source and remaining risks must be marked. This level embeds the capability domain of `document quality domain` through the six-document alignment proofreading subprocess; preceding lightweight capability domains are embedded through accepted full prerequisites.

#### 12.4.2 Input Scope and Writing Basis

Formal user manual generation must be based on `{{%PRIMARY_PUBLIC_ENTRY}}`, user-visible files in the release package, current stable implementation, and current stable facts in the first five controlled documents. Protected content in the protected three documents can only be used as constraints and writing basis; it must not be overwritten, migrated, weakened, or rewritten in reverse by manual generation, merge, review, six-document alignment proofreading, or ordinary version alignment. Manual structure, public entry chapter matrix, table fields, example granularity, and note expression should naturally unfold from this project's public exposure. API, CLI, SDK, service, plugin, protocol, configuration, user interface, data format, model entry, deployment, operations, and documentation entry chapters are enabled only when the corresponding public entry truly exists. The table of contents is not a fixed template and must be computed from current public entries, capability-domain grouping, and real body headings.

Writing rules, fact authority, user perspective, public entry chapter matrix, public definition style, conditional function-family templates, confidentiality boundaries, example signatures, and QA checks are governed by Chapter 13. Chapter 13 only explains how the manual body should be written. This section carries automatic inclusion, capability detection, subagent scheduling, task briefs, queuing, stop-and-resume, temporary drafts, merging, review, final release review, six-document alignment proofreading, protected-content gate for the protected three documents, output, and to-do plan boundaries.

#### 12.4.3 Subagent Orchestration Hard Constraints

Capability detection must be completed before execution. When nested subagents are supported, a three-layer physical architecture of session agent, documentation-writing coordinator subagent, and chapter writing/chapter merge/chapter review/six-document alignment proofreading subagents must be used. When only the session agent has subagent splitting capability and subagents cannot continue delegation, a two-layer sibling architecture must be used: first the documentation-writing coordinator subagent produces the chapter task brief and six-document alignment proofreading task brief, then the session agent starts sibling chapter writing, merge, review, and six-document alignment proofreading subagents according to the task briefs.

Before starting chapter writing, chapter merge, chapter review, or six-document alignment proofreading subagents, the maximum real subagent concurrency count and hard total cap supported by the current environment must be dynamically detected. A task dependency graph must be established among chapter task briefs, fact sources, temporary drafts, merge, review, protected-content gate for the protected three documents, and to-do plan writing, and explicit dependencies, implicit dependencies, cycle dependencies, same-fact-source dependencies, document read/write ownership, temporary draft ownership, merge writing ownership, and to-do plan write conflicts must be checked item by item. Only tasks with no dependency conflicts, no cycle dependencies, no read/write ownership conflicts, and no violation of chapter fact order, chain-level serial requirements, or protected gates may run in parallel inside the same phase. When conflicts exist, tasks must be reorchestrated as serial, split again, or stopped and reported; responsibilities must ***not*** be merged, write ownership shared, or prerequisite checks skipped to increase concurrency. Within the dynamically detected real concurrency cap, tasks that have passed the dependency and benefit gate above, can be split, can run in parallel, and can be independently accepted must be delegated to corresponding subagents as much as possible, while main-agent session context retains only task briefs, key findings, acceptance conclusions, blocking reasons, remaining queue, recovery entry, and final-report material.

As long as any subagent splitting capability exists, execution ***must not degrade to a single agent*** directly generating the full manual. When concurrency is insufficient, tasks must queue. Task count ***must not be reduced***, and multiple `##` major chapters, split units, six-document alignment proofreading domains, protected-content gate domains for the protected three documents, or independent review responsibilities ***must not be merged*** into the same subagent. When the hard total cap is exhausted while independent tasks remain incomplete, execution ***must stop and report***, preserving task brief, temporary draft status, six-document alignment proofreading status, protected-content gate status for the protected three documents, and remaining queue for continuation. When no real subagent capability exists at all, execution ***must stop and report***; it must not switch to file-based, phased, or per-chapter single-agent execution of the manual generation primary task. Public exposure lists, read-only fact calibration, quality checks, protected-content gate checks for the protected three documents, and pre-release read-only rechecks use `explore` or a subagent type with equivalent read-only capability. Chapter writing, temporary draft persistence, chapter merge, chapter review modifications, formal manual rewrite, allowed revisions inside six-document alignment proofreading, and to-do plan writing use `general` or a subagent type with equivalent read/write capability. If six-document alignment proofreading touches protected content in the protected three documents and exceeds the narrow version-metadata exception, the current task and subsequent tools, subagents, and automation chains ***must stop***, and confirmation must be requested according to the project-constraint document hard write gate in Chapter 10. The parent agent must not privately end incomplete subagents because they run long, temporarily produce no output, progress slowly, or wait in queue.

The six-document alignment proofreading subprocess is an embedded required task of `documentation release domain` and belongs to this level's internal acceptance. It is not equivalent to separately starting the lightweight automatic quality guard group's `document quality domain`. The checking and allowed-revision strength of this subprocess must be no weaker than Section 11.4, covering Markdown, layout, version number, updated date, aligned-document fields, language, grammar, fact-presentation norms, conceptual conflicts and ambiguity, number and unit consistency, reference chain integrity, anti-weakening gate integrity, protected-content gate integrity for the protected three documents, and article quality review. At the same time, according to manual-generation responsibilities, it additionally reads source code, public entries, public implementation, and user-visible external references already present in the manual body or registered as project public facts, calibrating units, lengths, intervals, parameters, return semantics, and external fact source accessibility for public API, CLI, SDK, service, plugin, protocol, configuration, user interface, data format, model entry, deployment, operations, and documentation entries involved in the formal manual. The six-document alignment proofreading subprocess must cover the Markdown, language, concept, numbers/units, reference chain, anti-weakening, and protected-three-documents gate checks of `document quality domain` in capability domain, but does not constitute rerunning `document quality domain`. This subprocess must not modify protected content in the protected three documents under the name of alignment, proofreading, format repair, or ordinary version alignment, and must not introduce unregistered external materials to replace project facts. The project-constraint document hard write gate must be executed when the narrow version-metadata exception is exceeded.

#### 12.4.4 Documentation-Writing Coordinator Responsibilities

The documentation-writing coordinator must first read all rules in Chapter 13, then establish the public exposure list, listing APIs, CLIs, SDKs, services, plugins, protocols, configurations, user interfaces, data formats, model entries, deployment entries, operations entries, documentation entries, and genuinely applicable conditional public macros, type aliases, structure fields, enum values, callback types, opaque handles, `{{%EXTERNAL_LINKAGE_MODEL}}` function families, `{{%PRIMARY_LANGUAGE}}` operators, overloaded functions, templates, and helper interfaces. Inapplicable entries must be marked "not applicable" and must not be fabricated. Then, according to current public entries, capability-domain grouping, real body headings, and user lookup paths, it divides major chapters and establishes chapter task briefs, while also establishing the six-document alignment proofreading task brief, protected-content gate list for the protected three documents, and quality review checklist.

The chapter task brief must use `##` major chapters in the formal manual body as the base coverage unit, listing each `##` major chapter title, chapter scope, public exposure coverage items, assigned independent chapter writing tasks, scheduling mode, queue status, temporary draft path, acceptance conditions, created subagent count, and remaining creatable count. Each `##` major chapter must be assigned at least one independent chapter writing task. When subagent splitting capability exists, that task must be executed by an independent subagent. If one `##` major chapter covers multiple capability domains, function-family groups, or a large public exposure surface, the coordinator must split further and assign an independent chapter writing task to each split unit.

The six-document alignment proofreading task brief must list the version number, updated date, aligned-document fields, index, factual responsibilities, reference chains, numbers and units, terminology, anti-weakening gates, confidentiality boundaries, protected-content gates for the protected three documents, and allowed revision scope for `README.md`, `AGENTS.md`, `agents/RULES.md`, `agents/BASE.md`, `agents/TODO.md`, and `doc/DOCUMENTATION.md`. This task brief must be completed before formal manual release, and final reports must separately list coverage scope, revision summary, unrevised items, to-do plan write status, protected-content gate result for the protected three documents, and remaining risks.

The coordinator collects the summary, temporary draft path, coverage scope, and open issues returned by each chapter writing task. After all chapter drafts pass acceptance, it arranges an independent chapter merge task. Before merge, the chapter task brief and chapter writing task return results must be checked. If any `##` major chapter or split unit lacks an independent chapter writing task, lacks a temporary draft, did not return coverage scope, or failed to meet draft acceptance conditions, the coordinator must reassign, fill, queue, or stop and report; it must not enter merge directly.

#### 12.4.5 Chapter Writing, Merge, Review, and Release

Chapter writing tasks can only be responsible for one `##` major chapter or one split unit assigned to them in the chapter task brief. They must not cover multiple `##` major chapters at once, write unassigned chapters, or modify temporary drafts from other chapter writing tasks. Chapter writing tasks must persist the responsible chapter draft as a temporary file under `{{%MANUAL_OUTPUT_DRAFT_DIRECTORY}}/`, and before exit return summary, temporary draft path, covered public exposure, uncovered items, blockers, and open issues. Temporary draft body text must not contain maintenance notes, generation rationale, internal rules, subagent scheduling flow, temporary draft explanations, or uncertainty statements.

Chapter merge tasks must execute only after all chapter writing tasks exit successfully or the phase ends and drafts pass coordinator acceptance. The merge task performs only file-level ordered merging; it does not perform semantic reading, content parsing, excerpt edits, polishing, or rewriting. After merge completes, the coordinator must arrange independent chapter review tasks to review, supplement, and modify the `doc/DOCUMENTATION.md` draft according to Chapter 13 constraints.

Chapter review tasks check at least public exposure coverage, required content for public entries or conditional function families, confidentiality boundaries, table-of-contents jumps, example publicness, API/ABI concept distinction, Markdown tables, code blocks, heading hierarchy, `{{%TEXT_LINE_ENDING_POLICY}}`, `{{%TEXT_ENCODING_POLICY}}`, EOF newline, lint rules, number and unit consistency, reference chain integrity, terminology consistency, logic chain integrity, and reader perspective consistency. Before final release, the coordinator must confirm that `doc/DOCUMENTATION.md` is the only formal release manual, public exposure coverage has no obvious gaps, qualitative principle descriptions at public-entry or conditional function-family level are complete, formal manual body text does not expose maintenance flow or temporary draft paths, version number, updated date, and aligned-document fields are aligned, table-of-contents jumps work, six-document alignment proofreading is complete, protected-content gate for the protected three documents passes, and Markdown and quality checks pass or risks are clearly explained.

Chapter temporary drafts are generation-time temporary artifacts, not formal release documents. Temporary drafts should be cleaned after release completes. If the user explicitly requests retaining temporary drafts, the final report must mark their temporary nature, and they must not be added to the formal manual table of contents or body references. If execution stops for continuation because the hard total cap is exhausted, the final report must list completed tasks, generated temporary drafts, incomplete tasks, remaining queue, continuation entry, and the constraint that tasks must not be merged.

#### 12.4.6 Modification Boundary, To-Do Plan, and Reuse

This domain may fully generate or broadly rewrite the body of `doc/DOCUMENTATION.md` according to Chapter 13 rules, and must verify the six controlled documents through the embedded six-document alignment proofreading subprocess, aligning version number, updated date, aligned-document fields, indexes, and non-protected quality revisions only within each document's responsibility and allowed scope. Responsibilities, factual boundaries, and rule body text in the protected three documents are only reported, or handled according to the project-constraint document hard write gate in Chapter 10. Manual generation or six-document alignment proofreading must not be written as requiring automatic rewriting of protected three-document responsibility summaries, factual boundaries, or rule body text. Chapter 13 must not be actively rewritten, compressed, summarized, or weakened under the name of refreshing the formal manual. Except for version number, updated date, and aligned-document fields, Chapter 13 rule body text must not be modified. When the user explicitly requests rule revision, the project-constraint document hard write gate in Chapter 10 must still be satisfied first, and no write may be persisted before confirmation. Index, table-of-contents, anchor, or link alignment inside the protected three documents is not part of the narrow version-metadata exception; when `README.md`, `AGENTS.md`, or `agents/RULES.md` is touched, the Chapter 10 project-constraint document hard write gate still must be executed. When protected content in the protected three documents is involved, six-document alignment proofreading, ordinary version alignment, Markdown/format repair, and manual generation must not bypass the Chapter 10 project-constraint document hard write gate.

When code, security, compatibility, test, or factual issues are found, do not modify code; only report and record according to the to-do plan boundary. Confirmed issues with evidence location, impact scope, and recommended action that need later handling are automatically submitted to `agents/TODO.md`. User-explicitly provided public exposure lists, controlled document fact lists, raw verification logs, or fact materials produced in the same round may be reused. Any chain-level judgment conclusions, acceptance results, finding lists, or to-do plan candidates must not be reused to replace this quality domain's own manual fact calibration, and conclusions from static analysis domain, global security domain, incremental difference domain, public impact domain, factual boundary domain, or document quality domain must not be reused to replace this level's checks. Fact conflicts that cannot be adjudicated, inaccessible external references, or insufficient source evidence must not be guessed and revised; they should be listed as remaining risks or to-do plan candidates.

## 13. Formal User Manual Writing Rules

This chapter is the rule source for writing `doc/DOCUMENTATION.md`, and must not be overwritten, replaced, or rewritten in reverse by formal manual body text, documentation release results, or temporary drafts. Before any task prepares to modify this chapter's body text, rule-fidelity and anti-weakening gates must be executed first. If it cannot be proven that the modification does not weaken rules, execution ***must stop and report***, and must not continue overwriting.

The anti-weakening gate in this chapter must not replace the project-constraint document hard write gate in Chapter 10. Any task preparing to modify protected content in the protected three documents, even if the reason is Markdown/format repair, ordinary version alignment, six-document alignment proofreading, factual boundary domain, document quality domain, or documentation release domain, must first follow the Chapter 10 hard gate. The narrow version-metadata exception is limited to version number, updated date, and aligned-document fields.

The following actions are rule weakening and are prohibited by default:

- Compressing the complete rules in this chapter into a summary, outline, short checklist, or small number of principles.
- Deleting or merging to a degree that makes original section responsibilities, templates, QA checks, or confidentiality boundaries disappear or become untraceable.
- Weakening strong constraints such as "must", "must not", "can only", and "stop and report" into "should", "may", or "try to".
- Deleting public exposure coverage, source awareness, public entry chapter matrix, conditional function-family templates, table-of-contents jumps, confidentiality boundaries, example signature checks, Markdown checks, or any gate in the quality-domain-level capability-adaptive subagent process of Chapter 12 `documentation release domain`.
- Reducing rule granularity, deleting example templates, or deleting check items on the grounds of "simplification", "deduplication", or "readability improvement".
- Using body content, output results, or temporary drafts from `doc/DOCUMENTATION.md` to overwrite, replace, or rewrite this chapter's rules in reverse.

The following only indicate modifiable types after passing the Chapter 10 project-constraint document hard write gate; no persisted modification is allowed before the hard gate is satisfied. Changes to this chapter are limited to:

- Strengthening constraints, adding missing rules, repairing ambiguity, or eliminating conflicts with `AGENTS.md`.
- Targeted correction following changes to public API, build facts, or documentation release flow.
- Reordering chapter structure, while preserving or strengthening original responsibilities, templates, QA checklists, and hard constraints.
- Repairing Markdown, typos, numbering, cross-references, version number, updated date, and aligned-document fields.

The following gates must be executed before and after modifying this chapter:

- This chapter must not be rewritten into a summary version with fewer than the current major structural units.
- Unless the user explicitly approves deletion, coverage of third-level and fourth-level headings after modification must remain 100%.
- Unless the user explicitly approves deletion, non-empty line count and rule item count must not decrease by more than 10% from before modification. If a metric is not applicable, the reason must be explained and heading coverage plus old-subsection mapping must be performed.
- If any subsection is deleted, merged, or reordered, an old-subsection to new-subsection mapping and constraint-fidelity explanation must be provided.
- It must be confirmed that Chapter 12 `documentation release domain` quality-domain-level capability-adaptive subagent process, public exposure coverage, public entry chapter matrix, conditional function-family templates, confidentiality boundaries, QA checklist, and protected-content gate for the protected three documents remain preserved or strengthened.

After each modification to this chapter, the audit summary must state: whether any subsection, template, check item, or strong constraint was deleted; whether any strong constraint was weakened; whether heading coverage is complete; whether key gates remain; whether protected content in the protected three documents was touched and whether the Chapter 10 hard gate was executed; if deletion exists, whether the user explicitly approved it and where the corresponding constraints migrated.

### 13.1 Writing Rule Position and Current Responsibility

This chapter only carries rules for how the body of `doc/DOCUMENTATION.md` should be written, reviewed, and accepted, including user perspective, fact authority, public entry chapter matrix, table-of-contents templates, conditional function-family explanation rules, public definition style, example rules, confidentiality boundaries, and QA checks. This chapter does not carry the quality-domain-level execution flow of `documentation release domain`, such as automatic inclusion, capability detection, subagent scheduling, task briefs, queuing, stop-and-resume, temporary drafts, merging, review, final release review, output, or to-do plan writing, and must not replace the protected-content gate for the protected three documents.

The quality-domain-level flow of `documentation release domain` is controlled by the Chapter 12 `documentation release domain` subsection. This chapter only defines writing results, review criteria, and acceptance gates for the formal user manual body. When maintaining this chapter, the quality-domain-level strong constraints in Chapter 12 on capability detection, three-layer/two-layer architecture, prohibition on active degradation, dynamic detection of the current environment's maximum real subagent concurrency, task dependency graph, explicit/implicit/cycle dependency checks, read/write ownership conflict isolation, maximizing safe parallelism, concurrency queuing, hard-cap stop-and-resume, stop-and-report when no real subagent capability exists, `explore` / `general` or equivalent capability subagent type assignment, public exposure list, chapter task brief, temporary drafts, merge, review, final release review, and temporary draft handling must remain visible, executable, and unweakened.

This chapter must preserve and strengthen the formal manual writing goals, reference table-of-contents template, public entry chapter matrix, conditional function-family templates, QA checks, confidentiality boundaries, public exposure coverage, and example rules. No maintenance may replace these rules with manual body text, output results, temporary drafts, summaries, out-of-template explanations, or external execution flows.

### 13.2 Formal User Manual Reference Table of Contents Template

This section is not the table of contents of Chapter 13 of this file, nor a fixed chapter numbering scheme. It is a reference template for generating the formal user manual table of contents when writing or rewriting `doc/DOCUMENTATION.md`. The formal manual must transform maintenance-side chapters, templates, and check items in this section into its own heading hierarchy in `doc/DOCUMENTATION.md`, and build the table of contents from current public entries, capability-domain grouping, and real body headings.

The formal manual must not contain expressions pointing to maintenance rules in this file, such as "Chapter 13 Formal User Manual Writing Rules", "the rules in this chapter", "reference table of contents template", "QA checklist", "generation rationale", or "maintenance flow". The user manual may use its own numeric numbering, but numbering only serves manual body lookup and must not let readers sense the existence of Chapter 13 of this file.

The reference table of contents should naturally evolve from the following hierarchy. Real headings and anchors must be generated from real headings in the formal manual and adjusted with the public exposure surface and applicable public entry matrix of `{{%PRIMARY_PUBLIC_ENTRY}}`. The example preserves the document H1 and `## Table of Contents` as manual structure, and table-of-contents entries themselves start by default from real body headings at `##` and below:

````markdown
# {{%PROJECT_NAME}} User Manual

## Table of Contents

- [1. Version Information and Reading Path](#{{%REAL_HEADING_ANCHOR}})
  - [1.1 Document Version](#{{%REAL_HEADING_ANCHOR}})
  - [1.2 Public Materials and Applicable Versions](#{{%REAL_HEADING_ANCHOR}})
- [2. Quick Start](#{{%REAL_HEADING_ANCHOR}})
  - [2.1 Prerequisites](#{{%REAL_HEADING_ANCHOR}})
  - [2.2 Minimal Example](#{{%REAL_HEADING_ANCHOR}})
- [3. Product Model and General Conventions](#{{%REAL_HEADING_ANCHOR}})
  - [3.1 Public Entry Chapter Matrix](#{{%REAL_HEADING_ANCHOR}})
  - [3.2 API, ABI, and Compatibility Terms](#{{%REAL_HEADING_ANCHOR}})
- [4. Acquisition, Configuration, and Runtime Preparation](#{{%REAL_HEADING_ANCHOR}})
- [5. Public Entry Reference](#{{%REAL_HEADING_ANCHOR}})
  - [5.1 {{%PUBLIC_ENTRY_GROUP_TITLE}}](#{{%REAL_HEADING_ANCHOR}})
    - [5.1.1 {{%PUBLIC_ENTRY_TITLE}}](#{{%REAL_HEADING_ANCHOR}})
- [6. Examples, Limits, Troubleshooting, and Appendix](#{{%REAL_HEADING_ANCHOR}})
````

The example only explains table-of-contents organization and does not mean the final manual must use the same headings, numbering, or chapter count. The default table of contents covers all real headings at `##` and below in the body, excluding the document H1 and `## Table of Contents` itself. If the instantiated project explicitly requires including H1, table-of-contents generation and check scripts must use one consistent policy. When public entries, public modules, function families, public types, object lifecycles, or capability boundaries are added, manual table-of-contents entries should be added, split, merged, or reordered.

### 13.3 Writing Goals and Boundaries

#### 13.3.1 Target Positioning

These rules guide writing the formal user manual for `{{%PROJECT_NAME}}`. The target manual should be searchable, executable, and verifiable like an engineering reference manual, rather than simply moving a public entry, generated comment, command help, or interface declaration into body text.

The formal user manual must answer four kinds of questions:

- How users obtain, install, configure, or enter published capabilities.
- How users understand public entries, objects, parameters, configurations, data, commands, interfaces, or UI.
- How users complete calls, operations, integration, deployment, or operations tasks through applicable public entries, including parameters, lifecycles, error boundaries, and verification methods.
- How users judge which capabilities are already public and which capabilities cannot be used as published capabilities.

#### 13.3.2 User Perspective

The manual targets release users. Body text should be based on user-visible facts in release packages, product entries, public documents, public entries, public commands, public configurations, public data formats, or public interfaces, and should not explain public capabilities through maintenance documents, development processes, test entries, build scripts, source organization, or repository structure.

When the manual needs to judge whether a capability is public, `{{%PRIMARY_PUBLIC_ENTRY}}` and public entry facts recorded in `agents/BASE.md` should be authoritative. Capabilities not exposed in public entries must not be written as published capabilities. When a public entry only exposes definitions, configurations, types, or enums but no corresponding callable, operable, or verifiable capability, it can only be written as a public definition or capability boundary.

When writing `doc/DOCUMENTATION.md` according to this chapter, chapters, templates, check items, and maintenance-side perspective in this chapter must be transformed into formal user manual context. The user manual only presents user-visible usage instructions, public entry references, programming or operation models, configurations, and capability boundaries. It must not copy this chapter's headings, writing rules, QA checklists, generation rationale, maintenance flow, internal rules, or template source verbatim into the user manual body.

`README.md`, `AGENTS.md`, `agents/RULES.md`, `agents/BASE.md`, and `agents/TODO.md` have a one-way transparent relationship to `doc/DOCUMENTATION.md`. The first five documents may constrain and calibrate the formal user manual. The formal user manual must not define the responsibilities, rules, facts, priorities, or future plans of the first five documents in reverse, and must not use manual body text to define code facts in reverse.

#### 13.3.3 No Material Trace Requirement

The final manual and these rules must not contain identifiable vendor names, product names, positioning evidence, or copied content from external reference materials, internal material sources, competitor materials, or source materials. The project's own public product name, brand name, release name, and user-visible materials are preserved according to real public facts. What may be borrowed is the organization method, table granularity, public entry template, and note expression of engineering manuals; no trace that lets readers infer specific materials may be retained.

#### 13.3.4 Fact Authority

Manual fact priority should be fixed as:

1. APIs, CLIs, SDKs, services, plugins, protocols, configurations, user interfaces, data formats, model entries, deployment entries, operations entries, and documentation entries publicly declared in `{{%PRIMARY_PUBLIC_ENTRY}}`.
2. Binaries, headers, packages, commands, examples, configurations, or explanations visible to users in the release package or product entry.
3. Externally observable behavior proven by the current stable implementation.
4. User-facing explanatory text.

Explanatory text must not define code or product facts in reverse. When the manual conflicts with public entries, revise the manual rather than treating the manual as an interface, command, service, or configuration definition.

#### 13.3.5 Module and Public Entry Source Awareness

`{{%PRIMARY_PUBLIC_ENTRY}}` is the authoritative entry for public APIs or public usage contracts, but call comments, command help, configuration descriptions, or declaration files inside it usually only carry necessary explanatory responsibility and are not a complete formal user manual fact source. Before writing a module, public entry, function family, command, configuration, service endpoint, data format, or public definition, the writer must not rely only on brief comments in public entries. The corresponding implementation, usage points, or public verification path must be read to understand real externally observable semantics.

The minimum granularity of source awareness or implementation awareness is the public exposure entry written into the manual. Writers should first establish a coverage list from public entries, itemizing genuinely applicable APIs, CLIs, SDKs, services, plugins, protocols, configurations, user interfaces, data formats, model entries, deployment entries, operations entries, documentation entries, and conditional public macros, type aliases, complex structures, public structures and fields, enums and enum values, callback types, opaque handles, `{{%EXTERNAL_LINKAGE_MODEL}}` function families, `{{%PRIMARY_LANGUAGE}}` operator overloads, overloaded mathematical functions, templates, and helper interfaces. Then they should read the corresponding implementation or usage points and verify parameter units, field semantics, ownership, aliasing limits, state advancement, lifecycles, return values, and boundary conditions. Buffer, creation, initialization, processing, reset, or destruction semantics are enabled only when the entry matrix confirms applicability.

When writing public exposure entries, if code indexes, symbol references, call relationships, or semantic retrieval are available, they should first be used to locate corresponding implementation, usage points, and public verification paths, then source reading or public entry facts should be used to recheck parameter units, field semantics, ownership, lifecycles, return values, and boundary conditions. Indexes are only for locating and coverage assistance, and index summaries, internal paths, source line numbers, private object names, or unrechecked implementation details ***must not*** be written into the formal user manual body.

Deep source reading, implementation reading, or public verification path checking is only used to calibrate the manual's understanding of public facts. The final manual can only write public, stable, user-observable behavior; it must not expose source paths, internal object names, source line numbers, internal flows, private caches, algorithm steps, test structures, or build structures.

If implementation behavior, public entry declarations, and brief comments are inconsistent, record the issue as documentation fact needing clarification or repair. Do not fill it by guessing, and do not write uncertain content as a published promise.

#### 13.3.6 API and ABI Concepts

API is a usage contract between users and code, system interfaces, or programmatic entries, describing how users understand, call, compose, or operate the corresponding public entry.

ABI is a contract between code and code, describing exported symbols, calling conventions, type layouts, link artifacts, and binary compatibility boundaries.

`{{%PRIMARY_PUBLIC_ENTRY}}` is the authoritative entry for public APIs or public usage contracts. Only when the project has export macros, calling conventions, structure layouts, function pointers, opaque handles, link artifacts, or binary compatibility promises does it contain ABI-sensitive facts. Public headers where applicable, SDK documentation, service descriptions, CLI help, or configuration files must not be simply called ABI entries.

### 13.4 Complete Multi-Level Table of Contents Rules

#### 13.4.1 Mandatory Table of Contents Scope

The formal user manual must contain a complete jumpable table of contents. The table of contents must not list only first-level headings or stop at module headings. By default, the table of contents must cover all real headings at `##` and below in the body, excluding the document H1 and `## Table of Contents` itself, including public entry subsections, type subsections, function-family subsections, command subsections, configuration subsections, and appendix subsections. Maintenance-side QA checks must not enter the formal user manual body table of contents.

Table-of-contents hierarchy must correspond level by level to body heading hierarchy. When the body contains `##`, `###`, `####`, or deeper headings, the table of contents must recursively list corresponding entries using the same parent-child relationship. Deep headings must not be flattened into the same-level list, capability-domain or module headings alone must not be listed, and generic entries such as "see this section" must not replace real subheadings.

If the body contains headings at `##` and below, corresponding entries must exist in the table of contents. After headings are added, deleted, renamed, or moved, the table of contents must be updated. If the instantiated project explicitly requires the table of contents to also list H1, table-of-contents generation and check scripts must use one consistent policy and must not include it in one place and exclude it in another.

The table of contents is not a fixed chapter blueprint. It should be computed from current public exposure, applicable public entry matrix, capability-domain grouping, user lookup paths, and real body headings. New capabilities must not be forced into unsuitable chapters just to reuse an old table of contents.

#### 13.4.2 Heading Hierarchy Rules

Recommended heading hierarchy:

| Level | Purpose | Rule |
| --- | --- | --- |
| `#` | Document title | Use only once in the whole document. |
| `##` | Major chapter | Used for version information, quick start, general conventions, public entry reference, feature chapters, limits, appendices, and similar content. |
| `###` | Subchapter | Used for capability domains, concept groups, public entry groups, or conditional function-family groups. |
| `####` | Entry-level heading | Used for concrete interfaces, commands, configurations, service endpoints, function families, structures, enums, or public entries. |
| `#####` | Fixed paragraph inside an entry | Used only when truly necessary for long entries. |

Deeper headings are not recommended. Content beyond five levels should become bold paragraphs, lists, or tables to reduce table-of-contents maintenance cost.

#### 13.4.3 Table of Contents Link Rules

Table-of-contents links should rely on Markdown heading auto-anchors or markdownlint-compatible forms, and must not use inline HTML anchors. Table-of-contents text should match heading text. Only when a heading is too long may the table of contents retain a synonymous short name, while keeping a recognizable correspondence near the heading.

The table of contents should use nested unordered lists. Each level indents by two spaces and tabs are not mixed. Table-of-contents nesting depth should match body heading depth. If body heading hierarchy changes, table-of-contents indentation and parent-child relationships must be updated accordingly.

#### 13.4.4 Table of Contents Self-Check Rules

Before each release, check:

- Table-of-contents entry count matches body heading count.
- Every table-of-contents link jumps to a real heading.
- There are no orphan headings, duplicate headings, or invalid anchors.
- Example headings in code blocks are not mistaken for body headings.
- The table of contents itself follows the same rules.

### 13.5 Overall Chapter Architecture

#### 13.5.1 Recommended Chapter Order

The formal user manual should follow the order "usable first, rules next, reference last":

1. Version information and reading path.
2. Quick start.
3. Programming model and general conventions.
4. Public entry chapter matrix, explaining which of API, CLI, SDK, service, plugin, protocol, configuration, user interface, data format, model entry, deployment, operations, and documentation entries apply and which do not.
5. Public definitions, configurations, types, objects, state, permissions, errors, and compatibility boundaries.
6. Reference chapters organized by capability domain or public entry.
7. Public entry index and public exposure coverage appendix.
8. Capability boundaries, special values, glossary, and user-visible reference materials.

This order moves horizontal rules earlier, avoiding repeated explanations of entry status, parameter direction, resource ownership, error boundaries, permissions, platforms, and limits in every public entry.

The above order is a recommended organization principle, not a fixed table-of-contents list. The number, names, and order of concrete module chapters should evolve with the public facts and applicable public entry matrix of `{{%PRIMARY_PUBLIC_ENTRY}}`.

#### 13.5.2 Guide Layer

The guide layer helps users complete the first verifiable use. Content should include obtaining public entries, installation or configuration, minimal example, permission or environment prerequisites, verification method, and reading path. Only when the project is a C/C++ native library does it include headers, language standards, linking method, and a minimal program using handle-style interfaces.

The guide layer should not expand all function signatures or discuss implementation details. Its task is to establish the shortest path to a successful call.

#### 13.5.3 Concept Layer

The concept layer defines project-wide common language, including API/ABI, public entry status, object lifecycle, parameter naming, data formats, permissions, error handling, special values, resource ownership, and compatibility boundaries. `{{%EXTERNAL_LINKAGE_MODEL}}`, `{{%PRIMARY_LANGUAGE}}` semantics, type suffixes, complex layouts, buffer aliasing, and handle lifecycles are enabled only when the C/C++ native library or binary compatibility model applies.

Every concept-layer rule should be reusable in later public entries.

#### 13.5.4 Reference Layer

The reference layer organizes entries by capability domain or public entry. Each capability domain first gives purpose, applicable scenarios, common flow, and input/output matrix, then enters concrete interfaces, commands, configurations, service endpoints, data formats, UI operations, or function families.

Function-family reference is a conditional extension for C/C++, SDK, or functional API projects. It should not mechanically copy every type-suffix version; instead, it should group by semantic differences. Separate expansion is needed only when parameter shape, lifecycle, or return semantics differ. Non-functional projects should use command, endpoint, configuration, resource, page, or workflow entries instead.

#### 13.5.5 Appendix Layer

The appendix layer carries content shared by public entries but unsuitable for body insertion, such as public exposure coverage tables, entry matrices, type suffix matrices, capability boundaries, special values, and glossary. Maintenance-side QA checklists are used only for writing self-checks and do not enter the formal user manual body.

The appendix is not a dumping ground for incomplete content. Non-public capabilities must not be packaged as a roadmap or imply availability.

#### 13.5.6 Chapter Evolution Mechanism

Each time the manual is rewritten or broadly updated, first rebuild the public exposure list from current public entries, then decide chapter structure. When public modules, public entries, function families, type systems, configuration items, commands, service endpoints, enum usages, object lifecycles, or example entries are added, chapters should be added, split, merged, or reordered.

Chapter evolution should follow user lookup paths: general rules first, stable capability-domain grouping, public entries close to their owning modules or entries, and appendices for coverage matrices and boundary explanations. Old tables of contents can only be historical references and must not constrain the new manual version.

### 13.6 Progression from Quick Start to Reference Entries

#### 13.6.1 Minimal Quick Start Loop

Quick start must provide a minimal loop: obtain the entry, complete required configuration, prepare input, call or operate one published capability, check the result, release resources, or exit the session. If the example uses a handle, session, connection, task, subscription, or other resource object, it must show the complete lifecycle of creation, use, reset, or destruction.

Examples do not aim to cover all type combinations; they should show correct call order and resource ownership.

#### 13.6.2 Transition from Example to Rules

Immediately after the quick example, explain:

- Which public entry the current minimal example uses, and whether inapplicable entries have been clearly marked.
- The boundary of API and ABI, service contract, CLI contract, SDK contract, configuration contract, or data-format contract.
- The direction, length, units, encoding, time zone, or format of input and output data.
- Who creates, owns, and destroys resource objects, sessions, handles, connections, tasks, or subscriptions.
- When internal buffers, tokens, sessions, connections, pagination cursors, or output objects need to be reacquired.

#### 13.6.3 Transition from Rules to Public Entries

Before entering public entry reference, provide an explanation of "how to find an entry": first locate the capability domain, then locate the API, CLI, SDK, service, plugin, protocol, configuration, user interface, data format, model entry, deployment, operations, documentation entry, or conditionally applicable function family, then choose type suffix, data layout, command parameters, resource object, handle-style, session-style, one-off call, or workflow mode.

This reduces the risk that users misuse neighboring public entries as equivalent entries.

### 13.7 Public Definitions, Macros, and Calling Convention Style

#### 13.7.1 Macro Categories

Public macros, constants, annotations, decorators, configuration keys, environment variables, or public definitions should be explained by category rather than listed in appearance order. Macros and calling conventions are conditional extensions for C/C++ native libraries, SDK headers, or binary compatibility models. When no such model exists, "not applicable" must be marked; public headers where applicable or a macro system must not be fabricated.

| Category | Example | Required Content |
| --- | --- | --- |
| Import/export and calling convention | `{{%IMPORT_EXPORT_MACRO_NAME}}`, `{{%CALLING_CONVENTION_MACRO_NAME}}` | Whether it affects exported symbols, calling conventions, and binary compatibility. |
| Multiple-definition control | `{{%MULTIPLE_DEFINITION_CONTROL_MACRO_NAME}}` | Whether it affects header-local public static objects and cross-translation-unit behavior. |
| Aliasing limit | `{{%ALIAS_RESTRICTION_MACRO_NAME}}` | Whether input and output may overlap, and whether users may override it. |
| Assertion and error helpers | `{{%BASIC_ASSERTION_MACRO_NAME}}`, `{{%CONTEXT_ASSERTION_MACRO_NAME}}` | User-visible behavior on failure. |
| IO and memory helpers | `{{%SAVE_HELPER_MACRO_NAME}}`, `{{%READ_HELPER_MACRO_NAME}}`, `{{%BUFFER_REALLOCATION_MACRO_NAME}}`, `{{%POD_REALLOCATION_MACRO_NAME}}` | Supported buffer shapes, ownership, and side effects. |
| Constants and utilities | `{{%PUBLIC_CONSTANT_NAME}}`, `{{%PUBLIC_UTILITY_MACRO_NAME}}`, `{{%PUBLIC_CONFIGURATION_KEY_NAME}}` | Numeric meaning, units, and applicable scenarios. |

#### 13.7.2 Macro Entry Template

Macro entries should contain: purpose, expanded user-visible semantics, whether users may predefine and override it, whether it affects API or ABI, examples, and notes.

Macro internal implementation mechanisms must not be written as algorithm details. Export macros, calling convention macros, and aliasing macros in particular should be explained from compatibility and call-contract perspectives.

#### 13.7.3 Calling Convention Description

Calling conventions are ABI-sensitive facts. The manual should state that public functions are exported through a unified calling convention. Calling convention changes must not be written as ordinary document updates. If a callback class does not explicitly carry a calling convention, record the current state according to the public function pointer signature, and do not add promises on your own.

### 13.8 Custom Data Structures, Type Aliases, and Enum Style

#### 13.8.1 Type Aliases

Type alias entries should state: name, underlying type, width or signedness intent, main purpose, and compatibility meaning when they appear in public function signatures, SDK methods, service payloads, configuration formats, or data formats.

For example, byte types, loop-count types, thread-count types, and timing types should be explained centrally to avoid users mistaking them for ordinary integers that can be freely substituted.

#### 13.8.2 Complex Structures

Complex structures are conditional extensions for numeric libraries, DSP projects, scientific computing libraries, or binary data formats. When the project exposes complex numbers, vectors, matrices, tensors, frames, packets, or fixed binary records, an independent section must be created. If absent, mark "not applicable". Each applicable structure states at least:

- Real-part field name and imaginary-part field name.
- Underlying scalar type of fields.
- `{ re, im }` order.
- Interpretation of elements in array buffers.
- Boundaries relative to language-library internal objects, containers, or implementation-related types.
- Whether it is an ABI-sensitive layout.

Complex structures or fixed layouts must not be explained as non-public acceleration formats, and alignment, byte order, padding, or internal layout not present in public entries must not be promised.

#### 13.8.3 Public Structures

Public structure entries should include field table, field ownership, pointer validity period, units, whether users may write it, whether the library fills it, and whether it remains valid across calls.

Recommended field table format:

| Field | Type | Direction | Description |
| --- | --- | --- | --- |
| `field` | `type` | input/output/borrowed | Explain field meaning, units, and lifecycle. |

For structures containing raw pointers, do not casually write that the caller frees them or that the library keeps them long-term. Each item must be explained according to the public contract. If public evidence is missing, write "explained only in the interface return description; release responsibility is not inferred".

#### 13.8.4 Public Enums

Public enum, status code, error code, fixed value set, or configuration enum entries should state: name, underlying type or representation, values, numeric values, applicable public entries, default or recommended value, and unknown-value handling.

The current public enums or fixed value sets of the instantiated project are determined by `agents/BASE.md` and public entry facts. The manual should list value names and value semantics, and must not infer non-public algorithms, unpublished capabilities, or internal implementation from enum names, status code names, or configuration names.

#### 13.8.5 Callback Types

Callback entries should state: signature, parameter directions, return value meaning, calling thread, conditions under which null is allowed, user-data ownership, and objects that must not be released during the callback.

Callbacks, event handlers, task closures, async notifications, hooks, or plugin entries should clearly state that the caller provides function addresses, object references, URLs, queues, channels, or handlers. The manual must not promise that the project copies closures, extends external object lifetimes, or implicitly holds user resources unless the public contract clearly states it.

#### 13.8.6 Opaque Handles

Opaque handles, sessions, connections, resource objects, task objects, or subscription objects write only lifecycle and public entries they can be passed into, not fields. Objects are created or acquired by same-family `{{%CREATE_ENTRY_VERB}}` and released or closed by same-family `{{%DESTROY_ENTRY_VERB}}`; callers must not dereference them, bypass public entries to release them, or handle them using `free`, `delete`, or equivalent internal release methods.

### 13.9 Standard Template for Public Entry References

#### 13.9.1 Public Entry Heading

Public entry headings should use capability short names, entry short names, or same-family short-name combinations, and should not mechanically include all type suffixes, command aliases, or parameter combinations. The first sentence under the heading uses a verb to describe purpose, such as "compute", "create", "write", "generate", "reset", "query", "configure", or "deploy".

Public entry headings should be stable for long-term table-of-contents and index maintenance.

#### 13.9.2 Fixed Entry Order

Each public entry should use the following order:

1. Purpose.
2. Principle description.
3. Syntax.
4. Entry, dependency, and visible artifacts.
5. Parameters.
6. Call flow.
7. Description.
8. Return value or error boundary.
9. Notes.
10. Example.
11. Related entries.

Entries with no return value, no output, or only side effects may omit the return-value table, but prerequisites, success flag, and failure behavior must be written clearly in the description.

#### 13.9.3 Syntax Grouping

When the same public entry has multiple type suffixes, command forms, request forms, configuration forms, or parameter forms, syntax should be grouped by Case:

- Case 1: standard call or standard operation.
- Case 2: in-place, batch, async, or streaming call.
- Case 3: resource, handle, session, or connection creation.
- Case 4: internal buffer, internal state, or system-managed resource handling.
- Case 5: external buffer, external configuration, external object, or external service binding.

Each Case lists only representative signature, command, request, configuration, or operation templates, and uses a matrix to list all available combinations. Do not copy many prototypes that differ only by suffix, command alias, or parameter arrangement and then repeat the same parameter explanation.

#### 13.9.4 Entry, Dependency, and Visible Artifacts

In the `{{%PROJECT_NAME}}` user manual, public entries should be written as `{{%PRIMARY_PUBLIC_ENTRY}}` or the instantiated project's real entries. If examples need extra packages, headers, commands, environment variables, service addresses, permissions, configurations, or runtime files, explain them locally in the example. Link libraries, dynamic libraries, packages, images, plugins, commands, or runtime files only use names visible to release users, not development directories.

#### 13.9.5 Related Entries

Related entries should be organized by lifecycle or operation relationship. For example:

- Creation entries relate to destruction or close entries.
- Processing entries relate to reset entries.
- Internal buffer, session, or task access entries relate to processing entries.
- Initialization entries relate to state reset entries.
- Generation entries relate to delay, reset, query, and destruction entries.

### 13.10 Parameter Semantics, Types, Units, and Data Conventions

#### 13.10.1 Parameter Table Fields

Parameter tables prefer two columns: parameter and description. When type, command, request, or configuration format already appears in syntax, do not repeat it in the table unless the parameter has multiple legal types, template forms, command forms, or configuration forms.

| Parameter | Description |
| --- | --- |
| `{{%OUTPUT_PARAMETER_NAMING_CONVENTION}}` | Output object, output buffer, or response object, provided by caller or system according to the public contract. |
| `{{%INPUT_PARAMETER_NAMING_CONVENTION}}` | Input object, input buffer, request body, configuration, or command parameter, valid during the call. |
| `{{%LENGTH_CAPACITY_PARAMETER_NAMING_CONVENTION}}` | Count, length, capacity, page size, or range parameter; units must be stated. |

#### 13.10.2 Required Contents of Parameter Descriptions

Each parameter description should cover as much as possible:

- Direction: input, output, input-output, borrowed, returned.
- Ownership: caller-owned, project-owned, system-owned, temporary borrow, handle-internal borrow, server-managed.
- Unit: elements, bytes, samples, seconds, Hz, radians, normalized frequency, entries, pages, requests, connections, tasks, or product-defined units.
- Boundary: whether 0 is allowed, whether null pointer, empty string, empty array, or empty object is allowed, enum legal values, lower length bound, pagination boundary, or timeout.
- Aliasing: whether input and output may overlap.
- Lifecycle: whether pointers remain usable after the call and when they become invalid.

#### 13.10.3 Aliasing, Overlap, and Shared Resources

Parameters with `{{%ALIAS_RESTRICTION_MACRO_NAME}}` or equivalent aliasing limits must be written as disallowing overlap. Parameters, request objects, files, connections, handles, sessions, caches, or external resources without aliasing limits must also not promise in-place safety, sharing safety, or concurrency safety by default unless public semantics clearly support it.

If a public entry provides `_Self`, input/output same-address, batch reuse, streaming reuse, shared session, or external resource binding versions, separately explain the difference from non-in-place or exclusive versions, allowed resource shapes, and update order.

#### 13.10.4 Length and Capacity

Length, capacity, range, pagination, batch size, timeout, window, or quota parameters must state units. In vector objects or container objects, `Count` is valid element count, `Capacity` is allocated capacity, `Ensure` only guarantees capacity, `Resize` changes valid element count, and `Realloc` changes capacity and storage location. Non-container projects should use the corresponding public terms and must not mechanically apply container semantics.

Any public entry that may change internal storage location, session state, pagination cursor, connection state, temporary file, cache location, or borrowed object validity must remind users to reacquire the corresponding resource or revalidate state.

### 13.11 Resource Lifecycle and State Object Description Template

#### 13.11.1 General Lifecycle

Handle-style, session-style, connection-style, task-style, or resource object interfaces should be written uniformly as:

```text
create/acquire -> prepare input/output -> process/call -> reset/continue -> destroy/close
```

If the public entry contains an initialization entry, write it as:

```text
create/acquire -> initialize -> process/call -> reset/continue -> destroy/close
```

If the public entry uses internal buffers, managed resources, or system state, write it as:

```text
create/acquire -> acquire input resource -> write input -> process/call -> acquire output resource -> read output -> destroy/close
```

#### 13.11.2 Creation and Destruction

`{{%CREATE_ENTRY_VERB}}` returns an opaque handle, session, connection, task, subscription, or resource object for resources owned by the project, system, or service. The caller only stores the public identifier and passes it back to same-family public entries; the caller must not dereference it or bypass public entries to access internal fields.

`{{%DESTROY_ENTRY_VERB}}` must match the public entry, resource type, and compatibility suffix of `{{%CREATE_ENTRY_VERB}}`. After `{{%DESTROY_ENTRY_VERB}}`, the handle, session, connection, internal buffer pointers, and borrowed objects returned by that resource all become invalid.

#### 13.11.3 Processing or Calling

`{{%PROCESS_ENTRY_VERB}}` should state input source, output destination, whether state advances, whether it can be called repeatedly, and whether it reads or writes the handle, session, task, connection, or internal buffer.

`{{%PROCESS_ENTRY_VERB}}`, `{{%RESET_ENTRY_VERB}}`, `{{%INITIALIZE_ENTRY_VERB}}`, `{{%INPUT_BIND_ENTRY_VERB}}`, `{{%OUTPUT_BIND_ENTRY_VERB}}`, and `{{%DESTROY_ENTRY_VERB}}` for the same resource object should be serialized by the caller unless the public contract clearly supports concurrency. Different resource objects may be used independently, but when they share the same external buffer, file, connection, session, or service quota, the caller still ensures coordination.

#### 13.11.4 Reset and Initialization

`{{%RESET_ENTRY_VERB}}` is written as resetting runtime state, not releasing resources, closing connections, or changing configuration. If the concrete rollback point of `{{%RESET_ENTRY_VERB}}` depends on the most recent `{{%INITIALIZE_ENTRY_VERB}}`, the manual should state that clearly.

`{{%INITIALIZE_ENTRY_VERB}}` is written as a configuration or state initialization entry. Public initialization parameters of the instantiated project must state units, ranges, and whether they affect later `{{%PROCESS_ENTRY_VERB}}`. For numeric or DSP projects, sampling, phase, frequency, decimation/interpolation factors, filter coefficients, recursive state, and other public parameters must also be covered. For service, CLI, SDK, or deployment projects, connection parameters, authentication context, cache strategy, task parameters, or equivalent public parameters must also be covered.

#### 13.11.5 Internal Buffer Borrowing

`{{%INPUT_RESOURCE_GET_ENTRY_VERB}}` and `{{%OUTPUT_RESOURCE_GET_ENTRY_VERB}}` return borrowed pointers, borrowed objects, pagination cursors, temporary URLs, task results, or system-managed resources, not internal resources owned by the caller. The manual must state:

- Borrowed objects are managed by handles, sessions, connections, tasks, or the system.
- The caller must not release or expand them.
- Borrowed objects become invalid after `{{%DESTROY_ENTRY_VERB}}`, connection close, task completion, cursor expiration, or the public invalidation point.
- They should be reacquired after function calls that may change internal storage.
- Input and output lengths are interpreted according to creation parameters and data types.

#### 13.11.6 External Buffer Binding

`{{%INPUT_BIND_ENTRY_VERB}}` and `{{%OUTPUT_BIND_ENTRY_VERB}}` mean binding caller-provided external buffers, files, objects, queues, connections, or configurations; they do not mean copying. The manual must state that external resources are prepared by the caller and remain valid during `{{%PROCESS_ENTRY_VERB}}`.

### 13.12 Conditional Public Entries, `{{%PRIMARY_LANGUAGE}}` Helper Interfaces, and Operator Overload Coordination

#### 13.12.1 `{{%EXTERNAL_LINKAGE_MODEL}}` Function Families

`{{%EXTERNAL_LINKAGE_MODEL}}` function families are conditional extensions for C/C++ native libraries, SDK headers, or binary compatibility models. When applicable, they should be written as public linked symbol families, not as `{{%PURE_LANGUAGE_SUBSET_COMPATIBILITY_MODEL}}` header compatibility. If public headers where applicable use `{{%PRIMARY_LANGUAGE_STANDARD_VERSION}}` semantics, a `{{%PURE_LANGUAGE_SUBSET_COMPATIBILITY_MODEL}}` compiler cannot directly understand all content as a C header. If not applicable, "not applicable" must be marked and function families must not be fabricated.

The `{{%EXTERNAL_LINKAGE_MODEL}}` chapter should cover exported symbols, calling conventions, base type layout, public structures, function pointers, opaque handles, and function-family lifecycles.

#### 13.12.2 `{{%PRIMARY_LANGUAGE}}` Public Semantics

`{{%PRIMARY_LANGUAGE}}` public semantics are placed in a separate section only when the project exposes language-level APIs, SDKs, plugin interfaces, or native libraries, including:

- Operator overloads for complex structures.
- Global overloaded mathematical function families.
- Templated save, read, and reallocation helper interfaces.
- Usage boundaries for header-local public static objects.
- `{{%PRIMARY_LANGUAGE_STANDARD_VERSION}}` language and standard library requirements.

These contents belong to public entries, APIs, or compatibility surfaces because user source, scripts, configurations, or plugins participate in parsing, instantiation, binding, or linking. However, they do not necessarily belong to `{{%BINARY_COMPATIBILITY_MODEL}}`.

#### 13.12.3 Operator Overloads

Operator overloads, extension methods, decorators, annotations, or language-level shortcut syntax entries should state supported types, operator or syntax sets, return types, whether the left operand is modified, whether scalar and complex mixing is allowed, whether fixed-point bitwise or shift semantics exist, and whether they are APIs or compatibility surfaces.

Operator overloads or language-level public semantics must not be hidden behind ordinary function families, and must not be omitted because they are not `{{%EXTERNAL_LINKAGE_MODEL}}` functions.

#### 13.12.4 Overloaded Mathematical Functions

Overloaded mathematical function families or domain shortcut functions should be grouped by semantics. Numeric or DSP projects may use groups such as complex construction, real/imaginary parts, magnitude/power, phase normalization, exponential/logarithm, decibel conversion, sign, and split. Non-numeric projects must replace these with the instantiated project's public domain operations of the same kind and must not retain inapplicable numeric groups.

Each function family should state supported input types, return types, units, special values, and precision boundaries. Unpublished combinations must not be mechanically filled across types.

#### 13.12.5 Templates and Helper Interfaces

Templates, generics, helper interfaces, shortcut commands, configuration helpers, or script helper interfaces should state accepted parameter shapes, type constraints, ownership, exception or assertion behavior, thread boundaries, and examples.

Helper interfaces must not be packaged as `{{%PROJECT_DOMAIN_SHORT_NAME}}` main entries or unpublished capabilities. They should be explained as public convenience APIs, public entry helper items, or part of the coverage appendix.

### 13.13 Module and Public Entry Organization Rules

#### 13.13.1 Capability Domain Grouping

The `{{%PROJECT_NAME}}` user manual should be organized by the instantiated project's real public capability domains and public entries, not by file appearance order, source directory order, or maintenance document order. It is recommended to first list currently public capabilities such as `{{%CAPABILITY_DOMAIN_NAME_1}}`, `{{%CAPABILITY_DOMAIN_NAME_2}}`, and `{{%CAPABILITY_DOMAIN_NAME_3}}`. If the project is a C/C++/DSP/numeric library, corresponding conditional extensions may list base support, public types, numeric objects, vector math, file IO, ring buffers, parallel scheduling, burst detection, frequency-domain utilities, difference and magnitude, timing recovery and phase lock, filtering, window functions, `{{%FINITE_IMPULSE_RESPONSE_FILTER_CAPABILITY_NAME}}` design, resampling, `{{%NUMERICALLY_CONTROLLED_OSCILLATOR_CAPABILITY_NAME}}`, sequences, differential encoding, and frequency conversion. Conditional example capability domains must not be written as default chapters for all projects.

#### 13.13.2 Type Suffix Matrix

The type suffix matrix is a conditional extension for functional API, SDK, or native library projects, and should be filled according to combinations actually exposed by function families. Different modules have different type matrices; a suffix supported by one module must not be mechanically copied into another module. Non-functional projects may replace this with a command matrix, endpoint matrix, configuration matrix, data-format matrix, or capability matrix.

Recommended matrix fields:

| Field | Meaning |
| --- | --- |
| Suffix or variant | Type suffix or variant in public function name, command name, endpoint name, configuration name, or data format. |
| Element type | Public type of input/output elements. |
| Complex shape | Real, complex, or fixed-point complex. |
| Call shape | One-off, in-place, handle-style, session-style, command-style, request-style, internal buffer, or external binding. |
| Notes | Scaling, rounding, state, or buffer differences. |

#### 13.13.3 Container, Vector, or Resource Object Function Families

Containers, vectors, or resource objects should be explained along lifecycle and capacity semantics: create, destroy, data access, capacity query, expand capacity, reallocate, clear, reset, append, remove, and swap.

Functions that return internal storage must remind users that later expansion, reallocation, clear, reset, append, remove, swap, or destruction may invalidate existing pointers.

#### 13.13.4 Frequency-Domain, Batch, or Plan Object Conditional Chapters

When the project exposes `{{%FREQUENCY_DOMAIN_TRANSFORM_FUNCTION_FAMILY}}`, `{{%INVERSE_FREQUENCY_DOMAIN_TRANSFORM_FUNCTION_FAMILY}}`, `{{%VARIABLE_FREQUENCY_TRANSFORM_FUNCTION_FAMILY}}`, batch plans, compute graphs, task plans, or other plan objects, write them as "create plan or object, prepare input and output, execute processing, read result, destroy object". Input/output shapes, lengths, and units must be explained family by family.

Internal transform algorithms, dependency implementations, or acceleration paths must not be written as behavior users can rely on.

#### 13.13.5 Streaming Processing, Filtering, Resampling, and Frequency Conversion

Streaming processing, filtering, resampling, and frequency-conversion function families or workflows should focus on how coefficients or configurations enter the object, how state advances, the meaning of `{{%CREATE_ENTRY_VERB}}`, `{{%PROCESS_ENTRY_VERB}}`, `{{%RESET_ENTRY_VERB}}`, and `{{%DESTROY_ENTRY_VERB}}`, input/output length relationships, decimation/interpolation factors, phase or frequency units, and whether streaming block calls are allowed.

#### 13.13.6 Sequences, Generators, and Coding

`{{%NUMERICALLY_CONTROLLED_OSCILLATOR_CAPABILITY_NAME}}`, `{{%LINEAR_FEEDBACK_SEQUENCE_CAPABILITY_NAME}}`, `{{%SPREAD_SPECTRUM_SEQUENCE_CAPABILITY_NAME}}`, differential encoding, differential decoding, token generation, task generation, batch generation, or other generator capabilities should state state advancement, reset, delay, recursive state, output object, and generation length. Explicit parameter generation and internal recursive-state generation should be explained separately, so users do not have to guess whether state changes.

### 13.14 Examples, Tables, Notes, and Cross-Reference Rules

#### 13.14.1 Example Rules

Examples must use already public entries and must not invent function names, commands, endpoints, configurations, type combinations, or unpublished capabilities. Examples should be short and complete, preferably showing one correct call or operation flow.

Handle-style, session-style, connection-style, or task-style examples must include destruction, close, or release steps. Internal buffer or managed resource examples must show acquiring input resources first, writing, processing, reading output, and destruction or close.

#### 13.14.2 Table Rules

Tables should keep columns short and column counts stable. Long descriptions go after tables and are not forced into cells. When a pipe character needs to be expressed in a table, escape it as `\|` or rewrite it as text.

Do not use inline HTML line breaks or merged cells. Complex structures should preferably use lists plus small tables.

#### 13.14.3 Note Block Rules

Note blocks use pure Markdown block quotes:

```markdown
> **Note:** The buffer pointer returned by this function is managed by the handle; the caller must not release it.
```

High-risk behavior uses "Warning". The same note block expresses only one risk level.

#### 13.14.4 Cross-References

Related entry lists should be sorted by call relationship, not alphabetically. Lifecycle entries preferentially link to each other. Initialization, size query, processing, reset, destruction, close, query, or rollback inside the same capability domain should form a closed loop.

### 13.15 Capability Boundaries, Non-Public Capabilities, and Confidentiality Boundaries

#### 13.15.1 Published Capabilities

Only capabilities visible in public entries and having public call, operation, configuration, deployment, or verification paths can be written as published capabilities. Public types, enums, macros, configuration items, commands, or pages themselves may be explained, but must not be used to imply that a complete function family, command family, service capability, or workflow already exists.

#### 13.15.2 Non-Public Capabilities

Capabilities that are not implemented, are skeletons, placeholders, internal only, or not exposed in public entries must not be written as published capabilities and must not be used in examples.

If a boundary must be explained, write "not within the public scope of this manual" and do not write plan promises.

Definitions, interfaces, commands, configurations, internal objects, handle hiding mechanisms, internal flows, and internal carrier details that are not exposed in public entries must not appear in the formal user manual. Even if these facts are found through source reading or implementation reading, they can only be used to calibrate public semantics.

#### 13.15.3 Confidentiality Boundary

The formal user manual must not expose non-public, maintenance-side, or development-side maintenance documents, development directories, build scripts, test entries, source files, internal object names, source line numbers, internal flows, private caches, thread locks, register-level optimization details, or unpublished dependencies. Public release packages, public headers, and public build/installation commands may be described within user-visible explanation boundaries, but must not expand into internal maintenance explanations.

Each public capability, public entry, or conditional function family should have a short qualitative principle description that helps users use it correctly; it must not become an implementation description. Principle descriptions only explain purpose, input/output relationship, applicable scenarios, call model, and user selection basis; they do not write algorithm steps, internal data structures, optimization paths, or source facts.

#### 13.15.4 Platform and Performance Boundaries

Platform, `{{%DATA_PARALLEL_ACCELERATION_BACKEND}}`, threading, and performance descriptions must be based on current public facts. They must not imply unverified hardware backends, non-public platforms, or unreleased acceleration paths.

Performance tips should be written as usage recommendations, not unconditional promises.

### 13.16 Reusable Markdown Templates

#### 13.16.1 User Manual Table of Contents Template

````markdown
# {{%PROJECT_NAME}} User Manual

## Table of Contents

- [1. Version Information](#1-version-information)
- [2. Quick Start](#2-quick-start)
  - [2.1 Obtain Public Entries](#21-obtain-public-entries)
  - [2.2 Minimal Example](#22-minimal-example)
- [3. Programming Model](#3-programming-model)
  - [3.1 API and ABI](#31-api-and-abi)
````

The table-of-contents template covers all real headings at `##` and below in the body by default, excluding the document H1 and `## Table of Contents` itself. The H1 and `## Table of Contents` in the example are only manual structure, not table-of-contents entries. The example is only format and does not mean the final manual only lists these items. If the instantiated project explicitly requires including H1, table-of-contents generation and check scripts must use one consistent policy.

#### 13.16.2 Module Chapter Template

````markdown
## Public Entry or Capability Domain Name

### Purpose

Explain what problem the module solves and which input/output scenarios it fits.

### Principle Description

Use a short qualitative paragraph to explain the input/output relationship, applicable scenarios, and user selection basis of this module's public entries; do not describe internal algorithm steps.

### Programming Model

Explain one-off calls, commands, service endpoints, SDK methods, handle-style objects, session objects, resource objects, configuration objects, data objects, or external resource binding. Internal buffers only apply in native-library, SDK, functional API, numeric library, or resource-capacity models.

### Common Input/Output and Public Parameters

| Parameter | Description |
| --- | --- |
| `{{%INPUT_PARAMETER_NAMING_CONVENTION}}` | Input object, request body, command parameter, configuration item, or input buffer for applicable entries. |
| `{{%OUTPUT_PARAMETER_NAMING_CONVENTION}}` | Output object, response object, result location, or output buffer for applicable entries. |
| `{{%LENGTH_CAPACITY_PARAMETER_NAMING_CONVENTION}}` | Count, length, capacity, pagination, or range parameter. |

### Public Entries

- [`{{%CREATE_OR_GET_ENTRY_IDENTIFIER}}`](#{{%CREATE_OR_GET_ENTRY_REAL_ANCHOR}})
- [`{{%PROCESS_OR_CALL_ENTRY_IDENTIFIER}}`](#{{%PROCESS_OR_CALL_ENTRY_REAL_ANCHOR}})
- [`{{%RESET_OR_CONTINUE_ENTRY_IDENTIFIER}}`](#{{%RESET_OR_CONTINUE_ENTRY_REAL_ANCHOR}})
- [`{{%DESTROY_OR_CLOSE_ENTRY_IDENTIFIER}}`](#{{%DESTROY_OR_CLOSE_ENTRY_REAL_ANCHOR}})
````

#### 13.16.3 Public Entry Template

````markdown
#### `{{%PUBLIC_ENTRY_IDENTIFIER}}`

Process one input object, execute one public operation, or return one public result.

##### Principle Description

Use qualitative language to explain how this public entry transforms input, state, and parameters into user-visible output. Do not write internal data structures, optimization paths, or source flows.

##### Syntax

```text
{{%PUBLIC_ENTRY_SYNTAX_OR_CALL_EXAMPLE}}
```

##### Parameters

| Parameter | Description |
| --- | --- |
| `{{%RESOURCE_OR_SESSION_PARAMETER_NAME}}` | Opaque handle, session, connection, task, or resource object returned by the same-family creation entry. |
| `{{%OUTPUT_PARAMETER_NAMING_CONVENTION}}` | Output object, output buffer, response object, or result location. |
| `{{%INPUT_PARAMETER_NAMING_CONVENTION}}` | Input object, input buffer, request body, configuration, or command parameter. |
| `{{%PROCESSING_RANGE_PARAMETER_NAMING_CONVENTION}}` | Processing count, page size, range, capacity, timeout, or other parameter with units. |

##### Call Flow

The call flow must be selected according to the public entry chapter matrix subsection or real anchor in the formal manual; all public entries must not be written mechanically as resource lifecycle flows.

| Entry Type | Flow Main Line |
| --- | --- |
| Stateless one-off call | Prepare input -> call public entry -> read result -> handle error |
| Resource/session lifecycle | Create or acquire -> initialize -> process or call -> reset or continue -> destroy or close |
| CLI/command flow | Prepare environment -> assemble command and parameters -> execute command -> check exit status and output |
| Service endpoint/request-response | Prepare authentication and request -> send request -> read response -> handle errors and retries |
| Configuration/data format | Locate file or object -> fill fields -> validate format -> apply or import |
| UI/workflow | Enter page or interface -> perform user action -> confirm result -> handle abnormal state |

##### Return Value

Explain the returned object, status code, or prerequisites when there is no return value.

##### Notes

> **Note:** Whether input and output may overlap, be shared, or be accessed concurrently must be explained according to this public entry's contract.

##### Example

```text
// Use public entries to show the minimal call flow.
```

##### Related Entries

- `{{%RELATED_PUBLIC_ENTRY_IDENTIFIER}}`
- `{{%RELATED_PUBLIC_ENTRY_IDENTIFIER}}`
- `{{%RELATED_PUBLIC_ENTRY_IDENTIFIER}}`
````

#### 13.16.4 Public Type Template

````markdown
#### `TypeName`

Explain the type purpose and where it appears.

| Field | Type | Direction | Description |
| --- | --- | --- | --- |
| `field` | `type` | input/output/borrowed | Field meaning, units, and lifecycle. |

##### ABI-Sensitive Notes

Explain whether field order, underlying type, layout, or function pointer signature affects binary compatibility.
````

#### 13.16.5 Macro Template

````markdown
#### `MACRO_NAME`

| Item | Content |
| --- | --- |
| Category | Export, calling convention, aliasing limit, assertion, IO, memory, or constant. |
| Purpose | Explain user-visible semantics. |
| Overridable | Explain whether users may predefine it. |
| Compatibility Impact | Explain whether it affects API or ABI. |
````

#### 13.16.6 Typed Public Entry Template

Public entry templates must first choose the type according to the entry matrix, then fill in the corresponding flow. Stateless one-off calls, CLI commands, service endpoints, configurations, data formats, interfaces, or documentation entries must not mechanically apply resource object lifecycle. Resource lifecycle, internal buffers, external buffer binding, destruction, or close semantics are enabled only when the entry matrix confirms applicability.

| Type | Required Description | Handling When Not Applicable |
| --- | --- | --- |
| Stateless one-off call | Input, output, error boundary, idempotence, minimal example. | Delete resource lifecycle, reset, destruction, and buffer chapters. |
| Resource/session lifecycle | Create, initialize, process, reset or continue, destroy or close, invalidation rules. | Do not retain an empty resource table. |
| CLI/command flow | Command format, parameters, environment, exit code, stdout, stderr. | Do not fabricate CLI entries. |
| Service endpoint/request-response | Endpoint, method, authentication, request, response, status code, retry semantics. | Do not fabricate service capability. |
| Configuration/data format | File or object location, fields, defaults, validation, compatibility. | Do not fabricate configuration items or data formats. |
| UI/workflow | Entry location, user action, visible result, permissions, and failure state. | Do not fabricate UI or console. |

#### 13.16.7 Resource Lifecycle Template

````markdown
#### Resource Lifecycle

```text
create/acquire -> initialize -> process/call -> reset/continue -> destroy/close
```

| Stage | Caller Responsibility | Project Responsibility | Invalidation Rule |
| --- | --- | --- | --- |
| Create/acquire | Store returned resource identifier. | Create object and resources. | Must not continue using after creation failure. |
| Process/call | Keep input and output valid. | Read input and write output. | State may advance. |
| Reset/continue | Call serially. | Reset runtime state. | Should not be interpreted as releasing resources. |
| Destroy/close | Call only once. | Release resources. | Resource object and borrowed objects all become invalid. |
````

#### 13.16.8 Data Object, Buffer, and Aliasing Template

This template is enabled only when the project has C/C++, SDKs, functional APIs, numeric libraries, resource-capacity models, file/network streams, paginated results, queues, caches, or equivalent public data objects. Non-code and non-resource-capacity projects should replace it with real commands, endpoints, pages, configurations, data formats, or workflow objects.

````markdown
#### Data Object and Buffer Conventions

| Object or Buffer | Ownership | Length Unit | Aliasing or Sharing Rule | Invalidation Rule |
| --- | --- | --- | --- | --- |
| Input object or input buffer | Caller or user | Elements, bytes, records, request body, or public unit | Explained by public entry, function family, command, or endpoint. | Must be valid during call, request, or processing. |
| Output object or output buffer | Caller, user, or project | Elements, bytes, records, response body, or public unit | Explained by public entry, function family, command, or endpoint. | Must be valid during call, request, or processing. |
| Internal buffer or managed object | Resource object | Elements or public unit | Must not be released or expanded. | Invalid after destruction, close, or reallocation. |
````

#### 13.16.9 API and ABI Boundary Template

````markdown
#### API and ABI Boundary

API is a usage contract between users and code, system interfaces, or programmatic entries, describing how users understand, call, operate, and compose corresponding public entries.

ABI is a contract between code and code, describing exported symbols, calling conventions, type layouts, link artifacts, and binary compatibility boundaries.

This section explains which content is source-level calling convention, service contract, command contract, configuration contract, or data-format contract, and which content is binary-compatibility-sensitive fact. Public headers where applicable, SDK documentation, service descriptions, CLI help, or configuration files must not be simply called ABI entries.
````

### 13.17 QA Checklist

#### 13.17.1 Table of Contents Check

- The default table of contents covers all real headings at `##` and below in the body, excluding the document H1 and `## Table of Contents` itself.
- The table of contents covers each level of subheading level by level, with hierarchy, indentation, and parent-child relationships matching the body headings.
- Table-of-contents links all match actual headings.
- The table of contents is updated after heading changes.
- Inline HTML anchors are not used.
- Example headings inside code blocks are not counted in the table of contents.

#### 13.17.2 Public Exposure Check

- General public entry checks cover genuinely applicable entry locations, user entry methods, public contracts, stability levels, inputs and outputs, error boundaries, limits, permissions or access control, and user-visible results among APIs, CLIs, SDKs, services, plugins, protocols, configurations, user interfaces, data formats, model entries, deployment entries, operations entries, and documentation entries.
- Conditional extension checks are enabled only when the project has C/C++, SDKs, binary ABI, functional APIs, numeric libraries, resource objects, buffers, session objects, or equivalent models, covering import/export macros, calling convention macros, assertion macros, type aliases, complex structures, public structures and fields, enums and enum values, callbacks, opaque handles, `{{%EXTERNAL_LINKAGE_MODEL}}` function families, `{{%PRIMARY_LANGUAGE}}` operator overloads, overloaded mathematical functions, templates, helper interfaces, buffers, and resource lifecycles. Projects where these are not applicable must mark "not applicable" and must not fabricate these entries.
- Function signatures, command syntax, endpoint paths, configuration keys, field names, data-format fields, model entries, documentation entries, type suffixes, parameter order, return types, and lifecycles follow real public entries.
- Non-public, placeholder, or internal-only capabilities are not written as published capabilities.

#### 13.17.3 Source Intent Check

- Every public exposure entry written into the manual has read the corresponding implementation, declaration, or usage point by module, public entry, entry group, function family, command, configuration, endpoint, interface, data format, model entry, documentation entry, or definition category.
- Parameter units, field semantics, ownership, aliasing limits, state advancement, lifecycle, return values, output results, and boundary conditions have been checked. Buffer semantics are enabled only when the project truly has the corresponding model.
- Source facts, implementation facts, or public verification results have been transformed into public usage semantics, without leaking source paths, internal object names, source line numbers, internal flows, private caches, algorithm steps, test structures, or build structures.
- Inconsistencies among public entry comments, command help, configuration descriptions, interface declarations, and implementation have been marked as documentation facts needing clarification or repair, and have not been guessed into published promises.

#### 13.17.4 API and ABI Check

- API and ABI are clearly defined and not mixed.
- `{{%EXTERNAL_LINKAGE_MODEL}}` and `{{%PURE_LANGUAGE_SUBSET_COMPATIBILITY_MODEL}}` header compatibility are not mixed; when not applicable, "not applicable" is marked.
- `{{%PRIMARY_LANGUAGE}}` public semantics are written as public entries, APIs, or compatibility surfaces rather than unconditionally as `{{%BINARY_COMPATIBILITY_MODEL}}`.
- ABI-sensitive facts are expanded only when the project has binary compatibility promises, and only around exported symbols, calling conventions, type layouts, enum underlying types, function pointers, structure field order, and link boundaries.

#### 13.17.5 Buffer and Lifecycle Check

- Every handle-style, session-style, connection-style, task-style, or resource object public entry has create, process, reset, destroy, or close explanations. Stateless one-off calls, CLI/commands, service endpoints, configuration/data formats, and UI/workflows are checked according to their own flows and must not apply resource lifecycle.
- Internal buffers, managed objects, temporary URLs, task results, or pagination cursors state borrowing relationships and invalidation conditions.
- External buffers, files, connections, configurations, or objects state caller ownership, length, and validity period.
- `{{%ALIAS_RESTRICTION_MACRO_NAME}}` or equivalent aliasing constraints are reflected in parameter descriptions.
- Capacity semantics such as `Count`, `Capacity`, `Ensure`, `Resize`, and `Realloc` are checked only when the project has containers, vectors, resource capacity, pagination, quotas, caches, queues, or equivalent public semantics, and it is confirmed that these semantics are not mixed. Projects where they are not applicable must mark "not applicable" and must not fabricate capacity models.

#### 13.17.6 Example Check

- Examples use only public entries.
- Examples contain necessary public entries, dependencies, permissions, configuration, or minimal context.
- Handle-style, session-style, connection-style, or task-style examples include destruction, close, or release steps.
- Examples do not invent unpublished type combinations, commands, endpoints, configurations, or capabilities.
- Examples do not depend on development directories, test entries, or build scripts.

#### 13.17.7 Markdown Check

- Inline HTML is not used.
- Formal user manual release drafts must not retain `{{%...}}` template placeholders, maintenance-side template explanations, or uninstantiated conditional extensions. Project facts that cannot be confirmed must stop processing before release; only confirmed inapplicable or unestablished public facts can be written as user-visible "not applicable" or "not established".
- Table column counts are stable.
- Table cells do not contain complex multi-paragraph content.
- Code block language tags are clear.
- The document passes table-of-contents link, table integrity, and basic lint checks.

#### 13.17.8 Confidentiality and Boundary Check

- Identifiable vendor names, product names, or positioning evidence from external reference materials, internal material sources, competitor materials, or source materials do not appear; the project's own public product name, brand name, release name, and user-visible materials are preserved according to real public facts.
- Maintenance documents, development directories, test entries, build scripts, source files, internal object names, source line numbers, handle hiding mechanisms, service internal routes, or implementation flows are not exposed.
- Formal manual body text does not point to Chapter 13 of this file, writing rules, reference templates, generation rationale, maintenance flow, or QA checklists.
- The formal user manual is not used to define the rules, facts, or priorities of `README.md`, `AGENTS.md`, `agents/RULES.md`, `agents/BASE.md`, or `agents/TODO.md` in reverse.
- Platform, `{{%DATA_PARALLEL_ACCELERATION_BACKEND}}`, thread, and performance descriptions are based only on current public facts.
- Algorithm principles are only qualitative descriptions and do not write implementation steps.

#### 13.17.9 Article Quality and Consistency Check

- Numbers, units, version numbers, chapter numbers, dates, ranges, interval openness/closedness, parameter lengths, and return semantics are consistent throughout. During manual generation, source code, public entries, and public implementation must be used to calibrate unit facts for user-visible public facts.
- Table-of-contents links, section references, public entry indexes, related entries, public exposure appendices, and capability boundary descriptions in the formal manual should form traceable reference chains, with no broken chains, reverse definition of code facts, or circular misdirection.
- Headings, paragraphs, lists, and tables should maintain the same hierarchy granularity. Conditions, exceptions, prohibitions, allowed items, inputs, outputs, call flows, and stop conditions should be executable and unambiguous.
- Terms remain consistent after their first definition. API, ABI, `{{%EXTERNAL_LINKAGE_MODEL}}`, public headers where applicable, public function families, commands, endpoints, configurations, sessions, handles, buffers, elements, samples, bytes, capacity, and similar concepts must not be mixed.
- Strong constraints, confidentiality boundaries, public exposure coverage, source awareness, example signature checks, and this chapter's anti-weakening gate must not be weakened for readability, simplification, or merging drafts.
- The `MD013` line-length rule in Markdown checks may be exempt according to project rules, but table, fence, table of contents, link, list, whitespace, `{{%TEXT_LINE_ENDING_POLICY}}`, `{{%TEXT_ENCODING_POLICY}}`, and EOF newline issues must not be skipped because of a line-length exemption.

### 13.18 Glossary

#### 13.18.1 API

API is a usage contract between users and code, system interfaces, or programmatic entries, and is one or more public entries. It focuses on how users obtain callable entries, choose types, call functions, execute commands, access services, understand parameters, manage resources, handle return values, and compose interfaces.

#### 13.18.2 ABI

ABI is a contract between code and code. It focuses on exported symbols, calling conventions, type layouts, structure field order, enum underlying types, function pointer signatures, link artifacts, and binary compatibility boundaries.

#### 13.18.3 `{{%EXTERNAL_LINKAGE_MODEL}}`

`{{%EXTERNAL_LINKAGE_MODEL}}` means symbols are exported or declared using specific linkage rules. It does not mean public headers where applicable can be directly included by a `{{%PURE_LANGUAGE_SUBSET_COMPATIBILITY_MODEL}}` compiler, and it does not eliminate `{{%PRIMARY_LANGUAGE}}` semantics in public headers where applicable. Projects where it is not applicable must mark "not applicable".

#### 13.18.4 Opaque Handle

An opaque handle is an object reference that users can only store and pass, and cannot dereference or release on their own. Sessions, connections, tasks, or resource objects may also use the same model. Its fields and resource layout are not part of the public API.

#### 13.18.5 Borrowed Pointer

A borrowed pointer or borrowed object is a resource returned by the project, service, system, or handle without transferring ownership to the caller. The caller may read, write, or use it during the agreed validity period, but must not release it, expand it, or keep it across invalidation points.

#### 13.18.6 Function Family

A function family is a group of functions sharing purpose, parameter model, and lifecycle, and is a conditional extension for functional API projects. Type suffixes, in-place versions, handle versions, and internal buffer versions should be explained together in the same function-family entry. Non-functional projects should use corresponding terms such as command family, endpoint group, resource group, or workflow group.

## Appendix

### Instantiation Checklist

This checklist is a representative verification item at the template stage. During instantiation or later template maintenance, the full text of this file **must first be scanned** for all valid `{{%...}}` placeholders and a deduplicated set established. This checklist ***must not replace*** full-text scan results. The ellipsis form `{{%...}}` is not counted as a fill-in item when it is only syntax explanation. After instantiation is complete, this entire section and `### Placeholder Checklist` ***must be deleted*** and must not remain in formal output.

This checklist is used only for instantiation verification of engineering rules inside this file. Maintenance tasks for other documents must not be merged into this checklist, and this checklist must not replace strong constraints in each chapter of this file.

- Fill in version, date, project name, project domain short name, primary language, primary runtime, public entries, and authoritative public entry fact source. Version number remains consistent inside the same rule file, and date uses the `{{%UPDATED_DATE}}` placeholder in YYYY-MM-DD format.
- Clarify public entries, API, ABI, binary compatibility model, external linkage model, pure-language-subset compatibility model, and "not applicable" boundaries. When the corresponding model does not exist, "not applicable" must be written; public headers, exported symbols, calling conventions, services, commands, configurations, or data formats must not be fabricated.
- Map public entry paths, base capability layer, core implementation layer, domain extension layer, third-party dependencies, runtime/test/demo/generation/maintenance entries, source or content root, temporary draft directory, build directory, output directory, installation artifact directory, package directory, and tool configuration directory to the project's real structure.
- Fill in public types, macros, assertions, aliasing, stream helpers, header-local static objects, handle carriers, public constants, configuration keys, public structure associated pointers, and public type layout rules; mark "not applicable" item by item when the corresponding public surface does not exist.
- Complete type suffixes, internal type suffixes, public parameter naming, input/output parameter naming, length/capacity parameter naming, processing range parameter naming, entry verbs, entry identifiers, real anchors, and related public entry identifiers, ensuring same-family function, command, endpoint, or configuration family naming remains consistent.
- Fill in data-parallel acceleration backends, vector instruction sets, compile gates, platform architectures, toolchains, build systems, build presets, build scripts, full verification, installation flows, automated tests, module tests, source collection, resource definitions, text encoding, and line-ending policies.
- Fill in rules for conditional function families or capability families such as frequency-domain transform, inverse frequency-domain transform, variable-frequency transform, frequency-domain dependencies, numerically controlled oscillator, filtering, spread spectrum sequences, linear feedback sequences, file IO, test/observability entries, base or domain utility functions, and capability domain names.
- Check automatic quality domain chains, task risk level, automatic quality-loop level, subagent orchestration, dynamic detection of the current environment's maximum real subagent concurrency, read/write isolation, stop and queuing, hard-cap stop-and-resume, to-do plan gates, document maintenance, text validation, formal user manual gates, and Chapter 13 templates. These rules can only be instantiated as executable constraints inside this file and must not be weakened into generic prompts.

### Placeholder Checklist

This checklist lists **at most 10** representative/key placeholders or categories. The complete handling scope is based on the valid `{{%...}}` full-text scan results for this file. When any placeholder is added, deleted, or renamed, handling rules **must be updated according to scan results**. The representative items below ***must not be the only maintained items***.

- Metadata: `{{%PROJECT_NAME}}`, `{{%DOCUMENT_VERSION}}`, `{{%UPDATED_DATE}}` in YYYY-MM-DD format
- Project, language, and runtime: `{{%PROJECT_DOMAIN_SHORT_NAME}}`, `{{%PRIMARY_LANGUAGE}}`, `{{%PRIMARY_LANGUAGE_OR_RUNTIME}}`, `{{%PRIMARY_LANGUAGE_STANDARD_VERSION}}`
- Public entries and compatibility models: `{{%PRIMARY_PUBLIC_ENTRY}}`, `{{%PUBLIC_ENTRY_AUTHORITY}}`, `{{%PUBLIC_ENTRY_PATH_OR_IDENTIFIER}}`, `{{%BINARY_COMPATIBILITY_MODEL}}`, `{{%EXTERNAL_LINKAGE_MODEL}}`, `{{%PURE_LANGUAGE_SUBSET_COMPATIBILITY_MODEL}}`
- Directory layering: `{{%BASE_CAPABILITY_LAYER_PATH_OR_IDENTIFIER}}`, `{{%CORE_IMPLEMENTATION_LAYER_PATH_OR_IDENTIFIER}}`, `{{%DOMAIN_EXTENSION_LAYER_PATH_OR_IDENTIFIER}}`, `{{%THIRD_PARTY_DEPENDENCY_PATH_OR_IDENTIFIER}}`, `{{%SOURCE_OR_CONTENT_ROOT}}`
- Build, installation, and tests: `{{%BUILD_SYSTEM}}`, `{{%MAIN_BUILD_ENTRY}}`, `{{%BUILD_PRESET_FILE}}`, `{{%DEFAULT_FULL_VERIFICATION_COMMAND}}`, `{{%AUTOMATED_TEST_ENTRY_PATTERN}}`, `{{%INSTALL_ARTIFACT_DIRECTORY}}`
- Public macros, public types, and resources: `{{%IMPORT_EXPORT_MACRO_NAME}}`, `{{%CALLING_CONVENTION_MACRO_NAME}}`, `{{%ALIAS_RESTRICTION_MACRO_NAME}}`, `{{%PUBLIC_TYPE_OR_ENUM_NAME}}`, `{{%INTERNAL_HANDLE_CARRIER_MECHANISM}}`
- Naming, suffixes, and parameters: `{{%FLOAT32_PUBLIC_TYPE_SUFFIX}}`, `{{%PUBLIC_PARAMETER_NAMING_CONVENTION_1}}`, `{{%INPUT_PARAMETER_NAMING_CONVENTION}}`, `{{%STATE_OBJECT_CONFIGURATION_PARAMETER_NAME}}`
- Entry verbs and entry identifiers: `{{%CREATE_ENTRY_VERB}}`, `{{%PROCESS_ENTRY_VERB}}`, `{{%RESET_ENTRY_VERB}}`, `{{%DESTROY_ENTRY_VERB}}`, `{{%PUBLIC_ENTRY_IDENTIFIER}}`
- Acceleration backends and capability families: `{{%DATA_PARALLEL_ACCELERATION_BACKEND}}`, `{{%BASE_VECTOR_ACCELERATION_ISA}}`, `{{%COMPATIBLE_VECTOR_ACCELERATION_ISA}}`, `{{%DEFAULT_VECTOR_ACCELERATION_ISA}}`, `{{%FREQUENCY_DOMAIN_TRANSFORM_FUNCTION_FAMILY}}`, `{{%CAPABILITY_DOMAIN_NAME_1}}`
- Text and manual templates: `{{%TEXT_ENCODING_POLICY}}`, `{{%TEXT_LINE_ENDING_POLICY}}`, `{{%PUBLIC_ENTRY_GROUP_TITLE}}`, `{{%REAL_HEADING_ANCHOR}}`
