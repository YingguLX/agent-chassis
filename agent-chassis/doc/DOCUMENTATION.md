# {{%PRODUCT_NAME}} User Manual

Document version: `{{%DOCUMENT_VERSION}}`

Applicable version: `{{%APPLICABLE_PRODUCT_VERSION}}`

Release date: `{{%RELEASE_DATE}}`

Document status: `{{%DOCUMENT_STATUS}}`

This document is written for end users, integration developers, and operations users. It describes released capabilities and public preview capabilities whose status is explicitly marked. It includes only public facts that users can obtain, verify, and execute.

Public entries include API, CLI, SDK, service, plugin, protocol, configuration, user interface, data format, model entry, deployment entry, operations entry, and documentation entry. The actual applicable scope is governed only by the public-entry matrix in section 3.1.

An uninstantiated document may keep `{{%...}}` fields as fill points. A published version must remove all placeholders, fill notes, and template-explanation traces. A published version must not contain internal process, internal orchestration, unpublished entries, or unverified capability commitments.

## Table of Contents

This table of contents is a superset for the uninstantiated version and must not be used unchanged as a published table of contents. During instantiation, fill the public-entry matrix in section 3.1 first, then trim both the table of contents and the body. Non-applicable entries must not retain whole chapters, sections, complete examples, index items, or troubleshooting items.

- [1. Version Information and Reading Path](#1-version-information-and-reading-path)
  - [1.1 Document Version](#11-document-version)
  - [1.2 Public Materials and Applicable Version](#12-public-materials-and-applicable-version)
  - [1.3 Recommended Reading Path](#13-recommended-reading-path)
  - [1.4 Applicability Boundary](#14-applicability-boundary)
  - [1.5 Document Conventions](#15-document-conventions)
- [2. Quick Start](#2-quick-start)
  - [2.1 Prerequisites](#21-prerequisites)
  - [2.2 Acquisition Method](#22-acquisition-method)
  - [2.3 Minimal Example](#23-minimal-example)
  - [2.4 Runtime Verification](#24-runtime-verification)
  - [2.5 Quick Checklist](#25-quick-checklist)
- [3. Product Model and General Conventions](#3-product-model-and-general-conventions)
  - [3.1 Public-Entry Matrix](#31-public-entry-matrix)
  - [3.2 Language, Platform, and Runtime Environment](#32-language-platform-and-runtime-environment)
  - [3.3 Inputs, Outputs, and Data Model](#33-inputs-outputs-and-data-model)
  - [3.4 Optional Prerequisites and Access Boundaries](#34-optional-prerequisites-and-access-boundaries)
  - [3.5 Error Handling and Diagnostics](#35-error-handling-and-diagnostics)
  - [3.6 Performance, Quotas, and Limits](#36-performance-quotas-and-limits)
  - [3.7 API and ABI Concepts](#37-api-and-abi-concepts)
- [4. Acquisition, Configuration, and Runtime Preparation](#4-acquisition-configuration-and-runtime-preparation)
  - [4.1 Acquisition Entry](#41-acquisition-entry)
  - [4.2 Configuration Items](#42-configuration-items)
  - [4.3 Environment Variables](#43-environment-variables)
  - [4.4 Release Package Structure](#44-release-package-structure)
  - [4.5 Version Changes and Removal](#45-version-changes-and-removal)
  - [4.6 Optional Security and Compliance Notes](#46-optional-security-and-compliance-notes)
- [5. Public Entry Reference](#5-public-entry-reference)
  - [5.1 Public Entry Overview](#51-public-entry-overview)
  - [5.2 Public Entry Groups](#52-public-entry-groups)
  - [5.3 Public Entry](#53-public-entry)
  - [5.4 Data Types, Configuration, and Resource Entries](#54-data-types-configuration-and-resource-entries)
  - [5.5 Event, Callback, Notification, or Audit Entries](#55-event-callback-notification-or-audit-entries)
  - [5.6 Pagination, Batch Processing, Asynchronous Tasks, or Workflows](#56-pagination-batch-processing-asynchronous-tasks-or-workflows)
  - [5.7 Public Entry Index](#57-public-entry-index)
- [6. Public Feature Chapters](#6-public-feature-chapters)
  - [6.1 Feature Group Overview](#61-feature-group-overview)
  - [6.2 Feature Entry](#62-feature-entry)
  - [6.3 Workflow](#63-workflow)
  - [6.4 Console, UI, and Interactive Entries](#64-console-ui-and-interactive-entries)
  - [6.5 Access Control, Quotas, and Audit](#65-access-control-quotas-and-audit)
- [7. Examples and Tutorials](#7-examples-and-tutorials)
  - [7.1 Example Organization](#71-example-organization)
  - [7.2 Example Entry](#72-example-entry)
  - [7.3 Common Scenarios](#73-common-scenarios)
  - [7.4 Example Verification Notes](#74-example-verification-notes)
- [8. Compatibility, Limits, and Boundaries](#8-compatibility-limits-and-boundaries)
  - [8.1 Support Matrix](#81-support-matrix)
  - [8.2 Version Compatibility](#82-version-compatibility)
  - [8.3 Known Limits](#83-known-limits)
  - [8.4 Non-Public and Uncommitted Items](#84-non-public-and-uncommitted-items)
  - [8.5 Migration Guide](#85-migration-guide)
  - [8.6 Change Log](#86-change-log)
- [9. Troubleshooting and FAQ](#9-troubleshooting-and-faq)
  - [9.1 Troubleshooting Entry](#91-troubleshooting-entry)
  - [9.2 Issue Entry](#92-issue-entry)
  - [9.3 Error Code Index](#93-error-code-index)
  - [9.4 FAQ Entry](#94-faq-entry)
- [10. Indexes and Appendices](#10-indexes-and-appendices)
  - [10.1 Public Entry Index](#101-public-entry-index)
  - [10.2 Glossary](#102-glossary)
  - [10.3 Unit, Format, and Protocol Conventions](#103-unit-format-and-protocol-conventions)
  - [10.4 References](#104-references)
  - [10.5 Pre-Use Checklist](#105-pre-use-checklist)

## 1. Version Information and Reading Path

This chapter explains the document version, applicable materials, intended readers, and public boundary. Readers should be able to locate the public capabilities covered by this document from user-obtainable releases, portals, packages, interfaces, or product UI.

### 1.1 Document Version

| Item | Content |
| --- | --- |
| Product name | `{{%PRODUCT_NAME}}` |
| Document version | `{{%DOCUMENT_VERSION}}` |
| Applicable product version | `{{%APPLICABLE_PRODUCT_VERSION}}` |
| Release date | `{{%RELEASE_DATE}}` |
| Document status | `{{%DOCUMENT_STATUS}}` |
| Intended readers | `{{%INTENDED_READERS}}` |
| Primary entry | `{{%PUBLIC_ENTRY}}` |

### 1.2 Public Materials and Applicable Version

List the user-accessible public materials, applicable product versions, and public entries on which this manual is based. Internal implementation comments, temporary design drafts, maintenance records, and unpublished plans are not user commitments.

- Release package or product entry: `{{%RELEASE_PACKAGE_OR_PRODUCT_ENTRY}}`
- Public programmatic entry: `{{%PUBLIC_PROGRAMMATIC_ENTRY_SOURCE}}`
- Public command or UI entry: `{{%PUBLIC_COMMAND_OR_UI_ENTRY}}`
- SDK package or dependency coordinate: `{{%SDK_PACKAGE_ID}}`
- Public change log: `{{%PUBLIC_CHANGELOG_SOURCE}}`

### 1.3 Recommended Reading Path

- First-time users: read chapter 2 and the applicable minimal example to complete one verifiable use.
- Integration developers: read chapters 3, 5, and 8 to confirm public entries, error handling, and compatibility boundaries.
- Operations users and administrators: read deployment, operations, security and compliance, quota, limit, and diagnostic sections only when the product provides deployment or operations entries.

### 1.4 Applicability Boundary

Describe only features, entries, commands, configuration, and constraints within `{{%RELEASED_CAPABILITY_SCOPE}}`. Public preview capabilities must explicitly mark status, limits, and compatibility commitments.

This document must not include internal object names, unpublished roadmap items, private diagnostic data, unpublished entries, internal flows, orchestration processes, or implementation details. Examples must show only user-obtainable calls, commands, configuration, UI operations, or deployment methods.

### 1.5 Document Conventions

| Convention | Meaning |
| --- | --- |
| `{{%CODE_STYLE}}` | Indicates a command, path, field, interface name, or configuration key. |
| `{{%REQUIRED_MARK}}` | Indicates that the user must provide the value. |
| `{{%OPTIONAL_MARK}}` | Indicates that the user may omit the value or use a default. |
| `{{%PREVIEW_MARK}}` | Indicates a public preview capability with limited stability and compatibility commitments. |

## 2. Quick Start

This chapter gives the steps required to complete one minimal verifiable use.

### 2.1 Prerequisites

| Prerequisite | Applicable | Requirement | Verification method |
| --- | --- | --- | --- |
| Account or license | `{{%ACCOUNT_OR_LICENSE_APPLICABLE}}` | `{{%ACCOUNT_OR_LICENSE_REQUIREMENT}}` | `{{%ACCOUNT_VERIFICATION_METHOD}}` |
| Runtime environment | `{{%RUNTIME_ENVIRONMENT_APPLICABLE}}` | `{{%RUNTIME_ENVIRONMENT_REQUIREMENT}}` | `{{%RUNTIME_ENVIRONMENT_VERIFICATION_METHOD}}` |
| Network or dependency | `{{%NETWORK_OR_DEPENDENCY_APPLICABLE}}` | `{{%NETWORK_OR_DEPENDENCY_REQUIREMENT}}` | `{{%DEPENDENCY_VERIFICATION_METHOD}}` |
| Permission | `{{%PERMISSION_APPLICABLE}}` | `{{%PERMISSION_REQUIREMENT}}` | `{{%PERMISSION_VERIFICATION_METHOD}}` |
| Logs or diagnostics | `{{%LOG_OR_DIAGNOSTIC_APPLICABLE}}` | `{{%LOG_OR_DIAGNOSTIC_REQUIREMENT}}` | `{{%LOG_OR_DIAGNOSTIC_VERIFICATION_METHOD}}` |
| Support entry | `{{%SUPPORT_ENTRY_APPLICABLE}}` | `{{%SUPPORT_ENTRY_REQUIREMENT}}` | `{{%SUPPORT_ENTRY_VERIFICATION_METHOD}}` |

### 2.2 Acquisition Method

Use this section to confirm where users obtain the product, service, document, package, or entry; how they verify the version; and which preparation method applies to the selected public entry.

```text
{{%ACQUISITION_COMMAND_OR_ENTRY}}
```

### 2.3 Minimal Example

```{{%EXAMPLE_LANGUAGE}}
{{%MINIMAL_VERIFIABLE_EXAMPLE}}
```

```text
{{%MINIMAL_EXAMPLE_EXPECTED_OUTPUT}}
```

### 2.4 Runtime Verification

| Check item | Expected result | If it fails, see |
| --- | --- | --- |
| Version check | `{{%VERSION_OUTPUT_EXAMPLE}}` | `{{%VERSION_CHECK_FAILURE_ENTRY}}` |
| Minimal call | `{{%MINIMAL_CALL_SUCCESS_MARK}}` | `{{%MINIMAL_CALL_FAILURE_ENTRY}}` |
| Configuration load | `{{%CONFIGURATION_LOAD_SUCCESS_MARK}}` | `{{%CONFIGURATION_FAILURE_ENTRY}}` |

### 2.5 Quick Checklist

- The applicable public entry has been acquired and prepared, including runtime preparation, login, configuration, or integration setup.
- Applicable authentication, permissions, network access, and dependent services are available.
- The minimal example has been run and the successful output has been recorded.
- The user knows where to find error codes, diagnostic information, and support entry points for the applicable entry.

## 3. Product Model and General Conventions

This chapter explains concepts that users need in order to read later public-entry and feature chapters.

### 3.1 Public-Entry Matrix

This section is the source of applicability for this manual. The table of contents, body, examples, indexes, and troubleshooting items must be trimmed from this matrix. A non-applicable entry must not keep a complete section, example, index, or troubleshooting item with a not-applicable note added afterward; it may only be described as not applicable in the matrix or be removed from the corresponding sections.

| Public entry | Applicable | Where users enter | Corresponding section | If not applicable |
| --- | --- | --- | --- | --- |
| API | `{{%API_APPLICABLE}}` | `{{%API_PUBLIC_ENTRY}}` | `{{%API_SECTION}}` | `{{%API_NOT_APPLICABLE_NOTE}}` |
| CLI | `{{%CLI_APPLICABLE}}` | `{{%CLI_PUBLIC_ENTRY}}` | `{{%CLI_SECTION}}` | `{{%CLI_NOT_APPLICABLE_NOTE}}` |
| SDK | `{{%SDK_APPLICABLE}}` | `{{%SDK_PUBLIC_ENTRY}}` | `{{%SDK_SECTION}}` | `{{%SDK_NOT_APPLICABLE_NOTE}}` |
| Service | `{{%SERVICE_APPLICABLE}}` | `{{%SERVICE_PUBLIC_ENTRY}}` | `{{%SERVICE_SECTION}}` | `{{%SERVICE_NOT_APPLICABLE_NOTE}}` |
| Plugin | `{{%PLUGIN_APPLICABLE}}` | `{{%PLUGIN_PUBLIC_ENTRY}}` | `{{%PLUGIN_SECTION}}` | `{{%PLUGIN_NOT_APPLICABLE_NOTE}}` |
| Protocol | `{{%PROTOCOL_APPLICABLE}}` | `{{%PROTOCOL_PUBLIC_ENTRY}}` | `{{%PROTOCOL_SECTION}}` | `{{%PROTOCOL_NOT_APPLICABLE_NOTE}}` |
| Configuration | `{{%CONFIGURATION_APPLICABLE}}` | `{{%CONFIGURATION_PUBLIC_ENTRY}}` | `{{%CONFIGURATION_SECTION}}` | `{{%CONFIGURATION_NOT_APPLICABLE_NOTE}}` |
| User interface | `{{%UI_APPLICABLE}}` | `{{%UI_PUBLIC_ENTRY}}` | `{{%UI_SECTION}}` | `{{%UI_NOT_APPLICABLE_NOTE}}` |
| Data format | `{{%DATA_FORMAT_APPLICABLE}}` | `{{%DATA_FORMAT_PUBLIC_ENTRY}}` | `{{%DATA_FORMAT_SECTION}}` | `{{%DATA_FORMAT_NOT_APPLICABLE_NOTE}}` |
| Model entry | `{{%MODEL_ENTRY_APPLICABLE}}` | `{{%MODEL_ENTRY_PUBLIC_ENTRY}}` | `{{%MODEL_ENTRY_SECTION}}` | `{{%MODEL_ENTRY_NOT_APPLICABLE_NOTE}}` |
| Deployment | `{{%DEPLOYMENT_APPLICABLE}}` | `{{%DEPLOYMENT_PUBLIC_ENTRY}}` | `{{%DEPLOYMENT_SECTION}}` | `{{%DEPLOYMENT_NOT_APPLICABLE_NOTE}}` |
| Operations | `{{%OPERATIONS_APPLICABLE}}` | `{{%OPERATIONS_PUBLIC_ENTRY}}` | `{{%OPERATIONS_SECTION}}` | `{{%OPERATIONS_NOT_APPLICABLE_NOTE}}` |
| Documentation entry | `{{%DOCUMENTATION_ENTRY_APPLICABLE}}` | `{{%DOCUMENTATION_ENTRY_PUBLIC_ENTRY}}` | `{{%DOCUMENTATION_ENTRY_SECTION}}` | `{{%DOCUMENTATION_ENTRY_NOT_APPLICABLE_NOTE}}` |

### 3.2 Language, Platform, and Runtime Environment

List `{{%SUPPORTED_LANGUAGES}}`, `{{%SUPPORTED_PLATFORMS}}`, `{{%RUNTIME_DEPENDENCIES}}`, and `{{%MINIMUM_VERSION_REQUIREMENTS}}`. If the product does not provide a class of entry, state not applicable and trim the corresponding section.

### 3.3 Inputs, Outputs, and Data Model

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `{{%FIELD_NAME}}` | `{{%FIELD_TYPE}}` | `{{%FIELD_REQUIRED}}` | `{{%FIELD_DESCRIPTION}}` |

Input conventions should list format, encoding, size limits, defaults, time zone, and units. Output conventions should list response structure, ordering, pagination, precision, null values, and error output.

### 3.4 Optional Prerequisites and Access Boundaries

This section lists only authentication methods, token locations, permission models, tenant isolation, and sensitive-data handling that are truly applicable. Non-applicable items are trimmed according to the section 3.1 matrix.

| Item | Content |
| --- | --- |
| Authentication method | `{{%AUTHENTICATION_METHOD}}` |
| Permission model | `{{%PERMISSION_MODEL}}` |
| Tenant boundary | `{{%TENANT_BOUNDARY}}` |
| Sensitive information rule | `{{%SENSITIVE_INFORMATION_RULE}}` |

### 3.5 Error Handling and Diagnostics

Error-handling conventions list error return shape, error-code naming, retry semantics, log locations, and diagnostic context.

```text
{{%ERROR_RESPONSE_EXAMPLE}}
```

### 3.6 Performance, Quotas, and Limits

| Limit category | Default | Adjustability | Description |
| --- | --- | --- | --- |
| `{{%LIMIT_CATEGORY}}` | `{{%LIMIT_DEFAULT}}` | `{{%LIMIT_ADJUSTABILITY}}` | `{{%LIMIT_DESCRIPTION}}` |

### 3.7 API and ABI Concepts

An API is a usage contract between users and code, system interfaces, or programmatic entries. An ABI is a binary contract between code units and is enabled only when exported symbols, calling conventions, type layouts, link artifacts, or binary compatibility commitments exist.

CLI, SDK, service, plugin, protocol, configuration, user interface, data format, model entry, deployment entry, operations entry, and documentation entry each use their own public contract and are not automatically classified as API or ABI.

## 4. Acquisition, Configuration, and Runtime Preparation

This chapter lists user-executable acquisition, configuration, runtime preparation, version-change, and removal methods. Entries that are not provided are marked through section 3.1 and do not form empty body sections. Deployment and operations sections are kept only when the matrix marks them as applicable.

### 4.1 Acquisition Entry

| Method | Scenario | Command or entry | Notes |
| --- | --- | --- | --- |
| `{{%ACQUISITION_OR_INSTALLATION_METHOD}}` | `{{%APPLICABLE_SCENARIO}}` | `{{%ACQUISITION_OR_INSTALLATION_ENTRY}}` | `{{%ACQUISITION_OR_INSTALLATION_NOTES}}` |

### 4.2 Configuration Items

| Item | Content |
| --- | --- |
| Name | `{{%CONFIGURATION_ITEM_NAME}}` |
| Type | `{{%CONFIGURATION_ITEM_TYPE}}` |
| Default | `{{%CONFIGURATION_ITEM_DEFAULT}}` |
| Required | `{{%CONFIGURATION_ITEM_REQUIRED}}` |
| Effective scope | `{{%CONFIGURATION_ITEM_SCOPE}}` |
| Example | `{{%CONFIGURATION_ITEM_EXAMPLE}}` |

### 4.3 Environment Variables

| Variable | Description | Default | Example |
| --- | --- | --- | --- |
| `{{%ENVIRONMENT_VARIABLE_NAME}}` | `{{%ENVIRONMENT_VARIABLE_DESCRIPTION}}` | `{{%ENVIRONMENT_VARIABLE_DEFAULT}}` | `{{%ENVIRONMENT_VARIABLE_EXAMPLE}}` |

### 4.4 Release Package Structure

```text
{{%RELEASE_PACKAGE_STRUCTURE_EXAMPLE}}
```

Every user-visible directory or file should list its responsibility. Do not describe implementation processes that users cannot see.

### 4.5 Version Changes and Removal

```text
{{%UPGRADE_ROLLBACK_REMOVAL_STEPS}}
```

### 4.6 Optional Security and Compliance Notes

This section lists only transmission encryption, storage, audit, privacy, license, and compliance boundaries that users need to know and that have been made public.

## 5. Public Entry Reference

This chapter organizes reference descriptions according to the applicable public entries in section 3.1. Public entries may be API, CLI, SDK, service, plugin, protocol, configuration, user interface, data format, model entry, deployment entry, operations entry, or documentation entry.

### 5.1 Public Entry Overview

| Public entry | User goal | Entry form | Status |
| --- | --- | --- | --- |
| `{{%PUBLIC_ENTRY_NAME}}` | `{{%PUBLIC_ENTRY_USER_GOAL}}` | `{{%PUBLIC_ENTRY_FORM}}` | `{{%PUBLIC_ENTRY_STATUS}}` |

### 5.2 Public Entry Groups

| Entry group | User goal | Entry form | Status |
| --- | --- | --- | --- |
| `{{%PUBLIC_ENTRY_GROUP_NAME}}` | `{{%PUBLIC_ENTRY_GROUP_USER_GOAL}}` | `{{%PUBLIC_ENTRY_GROUP_FORM}}` | `{{%PUBLIC_ENTRY_GROUP_STATUS}}` |

### 5.3 Public Entry

| Item | Content |
| --- | --- |
| Purpose | `{{%PUBLIC_ENTRY_PURPOSE}}` |
| Syntax or access method | `{{%PUBLIC_ENTRY_SIGNATURE_COMMAND_REQUEST_OR_ACCESS_EXAMPLE}}` |
| Parameters, options, or fields | `{{%PARAMETER_OPTION_OR_FIELD_DESCRIPTION}}` |
| Return, output, or result | `{{%RETURN_OUTPUT_OR_RESULT_DESCRIPTION}}` |
| Error boundary | `{{%ERROR_BOUNDARY_DESCRIPTION}}` |
| Example | `{{%PUBLIC_ENTRY_USAGE_EXAMPLE}}` |
| Related entries | `{{%RELATED_PUBLIC_ENTRIES}}` |

### 5.4 Data Types, Configuration, and Resource Entries

| Name | Fields | Value range | Compatibility notes |
| --- | --- | --- | --- |
| `{{%TYPE_CONFIGURATION_OR_RESOURCE_NAME}}` | `{{%FIELD_DESCRIPTION}}` | `{{%VALUE_RANGE}}` | `{{%COMPATIBILITY_NOTES}}` |

### 5.5 Event, Callback, Notification, or Audit Entries

Event semantics include trigger timing, delivery guarantees, retry strategy, ordering guarantees, idempotency advice, and payload structure.

```{{%EVENT_PAYLOAD_FORMAT}}
{{%EVENT_PAYLOAD_EXAMPLE}}
```

### 5.6 Pagination, Batch Processing, Asynchronous Tasks, or Workflows

This section lists pagination tokens, batch sizes, task states, polling or callback methods, timeouts, and cancellation semantics.

### 5.7 Public Entry Index

| Name | Type | Section | Status |
| --- | --- | --- | --- |
| `{{%PUBLIC_ENTRY_NAME}}` | `{{%PUBLIC_ENTRY_TYPE}}` | `{{%PUBLIC_ENTRY_SECTION}}` | `{{%PUBLIC_ENTRY_STATUS}}` |

## 6. Public Feature Chapters

This chapter organizes released and verifiable feature descriptions by user goal.

### 6.1 Feature Group Overview

| Feature group | User goal | Public entry | Status |
| --- | --- | --- | --- |
| `{{%FEATURE_GROUP}}` | `{{%FEATURE_USER_GOAL}}` | `{{%FEATURE_PUBLIC_ENTRY}}` | `{{%FEATURE_STATUS}}` |

### 6.2 Feature Entry

Each feature entry should explain scenario, prerequisite, operation, result, and limits. Unpublished, unverified, or internal-only capabilities must not be written as entries in this chapter.

### 6.3 Workflow

```text
{{%WORKFLOW_STEPS}}
```

### 6.4 Console, UI, and Interactive Entries

| UI entry | User action | Result |
| --- | --- | --- |
| `{{%UI_ENTRY}}` | `{{%UI_USER_ACTION}}` | `{{%UI_RESULT}}` |

### 6.5 Access Control, Quotas, and Audit

| Item | Description |
| --- | --- |
| Access control | `{{%ACCESS_CONTROL_DESCRIPTION}}` |
| Quota | `{{%QUOTA_DESCRIPTION}}` |
| Audit | `{{%AUDIT_DESCRIPTION}}` |

## 7. Examples and Tutorials

This chapter provides examples that users can copy, run, and verify.

### 7.1 Example Organization

| Example | Scenario | Public entry | Verification method |
| --- | --- | --- | --- |
| `{{%EXAMPLE_NAME}}` | `{{%EXAMPLE_SCENARIO}}` | `{{%EXAMPLE_PUBLIC_ENTRY}}` | `{{%EXAMPLE_VERIFICATION_METHOD}}` |

### 7.2 Example Entry

An example entry should explain background, preparation, steps, full code or command, expected output, verification method, and extended scenarios. Examples must not depend on internal entries, temporary paths, unpublished configuration, or uncommitted behavior.

```{{%EXAMPLE_LANGUAGE}}
{{%COMPLETE_EXAMPLE}}
```

### 7.3 Common Scenarios

| Scenario | Recommended entry | Reference section |
| --- | --- | --- |
| `{{%COMMON_SCENARIO}}` | `{{%RECOMMENDED_ENTRY}}` | `{{%REFERENCE_SECTION}}` |

### 7.4 Example Verification Notes

Example results may vary by version, permission, configuration, network, data scale, and runtime environment. Each example should give a clear expected result and a failure-diagnosis entry.

## 8. Compatibility, Limits, and Boundaries

This chapter lists support range, compatibility commitments, limits, migration, and change log.

### 8.1 Support Matrix

| Item | Support range | Description |
| --- | --- | --- |
| `{{%SUPPORT_ITEM}}` | `{{%SUPPORT_RANGE}}` | `{{%SUPPORT_DESCRIPTION}}` |

### 8.2 Version Compatibility

| Compatibility category | Commitment | Exception |
| --- | --- | --- |
| `{{%COMPATIBILITY_CATEGORY}}` | `{{%COMPATIBILITY_COMMITMENT}}` | `{{%COMPATIBILITY_EXCEPTION}}` |

Deprecation policy should list the deprecation marker, replacement, transition period, and removal condition.

### 8.3 Known Limits

| Limit | Impact | Recommendation |
| --- | --- | --- |
| `{{%KNOWN_LIMIT}}` | `{{%LIMIT_IMPACT}}` | `{{%LIMIT_RECOMMENDATION}}` |

### 8.4 Non-Public and Uncommitted Items

- Unpublished entries are not usable capabilities.
- Roadmap items not marked as public preview are not compatibility commitments.
- Internal implementation, internal diagnostics, private configuration, and maintenance tools are not user-dependable interfaces.

### 8.5 Migration Guide

```text
{{%MIGRATION_STEPS_AND_VERIFICATION_METHOD}}
```

### 8.6 Change Log

| Version | Date | Change | Compatibility impact |
| --- | --- | --- | --- |
| `{{%CHANGE_VERSION}}` | `{{%CHANGE_DATE}}` | `{{%CHANGE_DESCRIPTION}}` | `{{%COMPATIBILITY_IMPACT}}` |

## 9. Troubleshooting and FAQ

This chapter helps users locate common issues and collect support information.

### 9.1 Troubleshooting Entry

| Issue type | First place to check | Description |
| --- | --- | --- |
| `{{%ISSUE_TYPE}}` | `{{%FIRST_CHECK_ENTRY}}` | `{{%TROUBLESHOOTING_DESCRIPTION}}` |

### 9.2 Issue Entry

An issue entry should contain symptoms, possible causes, diagnostic steps, resolution, and information to provide when contacting support.

```text
{{%DIAGNOSTIC_STEPS_AND_RESOLUTION}}
```

### 9.3 Error Code Index

| Error code | Category | Meaning | Handling suggestion |
| --- | --- | --- | --- |
| `{{%ERROR_CODE}}` | `{{%ERROR_CATEGORY}}` | `{{%ERROR_MEANING}}` | `{{%ERROR_HANDLING_SUGGESTION}}` |

### 9.4 FAQ Entry

| Question | Answer |
| --- | --- |
| `{{%FAQ_QUESTION}}` | `{{%FAQ_ANSWER}}` |

## 10. Indexes and Appendices

This chapter lists searchable indexes, terms, format conventions, references, and the pre-use checklist.

### 10.1 Public Entry Index

| Entry | Type | Section | Description |
| --- | --- | --- | --- |
| `{{%PUBLIC_ENTRY_NAME}}` | `{{%PUBLIC_ENTRY_TYPE}}` | `{{%PUBLIC_ENTRY_SECTION}}` | `{{%PUBLIC_ENTRY_DESCRIPTION}}` |

### 10.2 Glossary

| Term | Definition |
| --- | --- |
| API | Usage contract between users and code, system interfaces, or programmatic entries. |
| ABI | Binary contract between code units, enabled only when binary compatibility commitments exist. |
| Public entry | User-visible, user-obtainable, and user-verifiable API, CLI, SDK, service, plugin, protocol, configuration, user interface, data format, model entry, deployment entry, operations entry, or documentation entry. |
| Public preview | Public capability with limited compatibility commitments; its limits must be clearly marked. |

### 10.3 Unit, Format, and Protocol Conventions

| Category | Convention | Example |
| --- | --- | --- |
| `{{%CONVENTION_CATEGORY}}` | `{{%CONVENTION_CONTENT}}` | `{{%CONVENTION_EXAMPLE}}` |

### 10.4 References

List user-accessible public materials, standards, protocols, product pages, or example repositories.

- `{{%REFERENCE_NAME}}`: `{{%REFERENCE_LINK_OR_LOCATION}}`

### 10.5 Pre-Use Checklist

- The manual version applies to the current product version.
- The product's actual public entries have been confirmed, and the corresponding sections have been selected according to section 3.1.
- The applicable public entry has been acquired and prepared, including runtime preparation, authentication, access control, network, configuration, and dependent service setup.
- At least one minimal example for an applicable public entry has been run, and the verifiable result has been saved.
- The limits, error codes, diagnostic information, and support entry for the actual applicable entry are understood.
- No unpublished entry, internal implementation detail, or uncommitted behavior is being relied upon.
- All `{{%...}}` placeholders, fill notes, and template-explanation traces have been removed.
