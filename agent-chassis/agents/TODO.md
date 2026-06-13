# `{{%PROJECT_NAME}}` Follow-Up Implementation Plan

## 1. Version Information

- Current version: `{{%DOCUMENT_VERSION}}`
- Updated: `{{%UPDATED_DATE}}`
- Synchronized documents: `README.md` `{{%DOCUMENT_VERSION}}`, `AGENTS.md` `{{%DOCUMENT_VERSION}}`, `agents/RULES.md` `{{%DOCUMENT_VERSION}}`, `agents/BASE.md` `{{%DOCUMENT_VERSION}}`, `agents/TODO.md` `{{%DOCUMENT_VERSION}}`, `doc/DOCUMENTATION.md` `{{%DOCUMENT_VERSION}}`
- Analysis scope: `{{%PRIMARY_PUBLIC_ENTRY}}`, `{{%SOURCE_OR_CONTENT_ROOT}}`, `{{%RUNTIME_ENTRY}}`, `{{%BUILD_ENTRY}}`, `{{%TEST_ENTRY}}`, `{{%INSTALL_OR_RELEASE_ENTRY}}`, `README.md`, `AGENTS.md`, `agents/RULES.md`, `agents/BASE.md`, `doc/DOCUMENTATION.md`

## 2. Document Role

`agents/TODO.md` is the project's follow-up implementation plan and known issue record. It carries confirmed known issues, priorities, evidence locations, issue descriptions, impact scope, current exposure surface, first actions, and verification recommendations identified from unfinished or pending modules, `incremental difference domain`, `public impact domain`, `incremental security domain`, `global security domain`, `factual boundary domain`, `document quality domain`, `static analysis domain`, `documentation release domain`, build verification, test verification, or user feedback.

This file does not carry agent control rules, detailed engineering specifications, automatic quality guard processes, user manual writing rules, the complete project factual baseline, or the formal user manual. Agent control entry is governed by `AGENTS.md`; detailed engineering specifications, automatic quality guard processes, and user manual writing rules are governed by `agents/RULES.md`; project facts are governed by `agents/BASE.md`; the project summary is governed by `README.md`; the formal user manual is governed by `doc/DOCUMENTATION.md`.

## 3. Reading Guide

| Priority | Meaning | Handling principle |
| --- | --- | --- |
| P0 | Confirmed issue that blocks release, breaks compatibility, misleads user boundaries, creates security risk, or makes a core flow unavailable. | Handle first; evidence, impact scope, and verification results must be recorded before and after handling. |
| P1 | Confirmed issue affecting core capabilities, primary user paths, primary maintenance paths, or critical verification paths. | Complete design, implementation, testing, and documentation synchronization as soon as possible. |
| P2 | Confirmed issue affecting secondary capabilities, conditional technology stacks, integration quality, or documentation accuracy. | Schedule for a later iteration, and confirm scope and compatibility before handling. |
| P3 | Confirmed low-priority plan, experience improvement, test enhancement, documentation supplement, or user feedback suggestion. | Handle after requirements are clear, resources allow, or related modules have stabilized. |

Issue recording rules: a to-do plan may come from the automatic quality loop, build/test verification, document quality domain, and user feedback. Concrete automatic inclusion rules, chain-level order, permission boundaries, subagent orchestration, dependency graph, read/write ownership, and acceptance rules are governed by `AGENTS.md` / `agents/RULES.md`; this document ***must not copy*** the detailed quality-chain execution protocol. To-do plan records keep only `ID`, `Priority`, task risk level, automatic quality-loop level, source quality domain, prerequisite domain status, acceptance status, risk dimension, issue description, evidence location, impact scope, current exposure surface, first action, verification recommendation, and status. Chain levels that have not started, failed, are blocked, or await decision ***must not fabricate*** results. Unverified guesses, tool false positives, complete per-work-unit logs, low-confidence hints, and generic risk hints should not be mechanically written.

When a complex ordinary task produces to-do plan candidates, the recording scope must trace confirmed facts, explicit assumptions, uncleared blockers, user adjudication items, candidate approaches, acceptance items, and recovery entries. This information may only supplement evidence for issue description, first action, verification recommendation, or status scope, and ***must not*** copy the underlying fact derivation protocol from `agents/RULES.md` into the to-do plan body.

When the same issue is found from multiple sources, sources should be deduplicated and merged instead of registering duplicate records. When later levels have not started because an earlier level failed, was blocked, was interrupted by a hard limit, or required user judgment, only issues confirmed by completed levels may be recorded; findings or acceptance results for unstarted levels must not be fabricated.

Every confirmed to-do plan item **must have** `ID`, `Priority`, task risk level, automatic quality-loop level, source quality domain, prerequisite domain status, acceptance status, risk dimension, issue description, evidence location, impact scope, current exposure surface, first action, verification recommendation, and status. Issues that are incomplete, unverified, or not located ***must not be written as completed***.

Before closing, downgrading, merging, or deleting a to-do plan item, the corresponding evidence, verification result, and affected documents must be stated. Still-valid confirmed issues must not be deleted merely to keep tables concise.

## 4. To-Do Plan Summary Table

| Priority | task risk level | automatic quality-loop level | Risk dimension | Issue domain/module/item | File + line number | To-do plan summary | Impact scope | Current exposure surface |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `{{%TO_DO_PRIORITY}}` | `{{%TASK_RISK_LEVEL}}` | `{{%AUTOMATIC_QUALITY_LOOP_LEVEL}}` | `{{%RISK_DIMENSION}}` | `{{%CAPABILITY_OR_PROBLEM_DOMAIN}}` | `{{%EVIDENCE_LOCATION}}` | `{{%TO_DO_SUMMARY}}` | `{{%IMPACT_SCOPE}}` | `{{%CURRENT_EXPOSURE_SURFACE}}` |

When there are no confirmed issues, this table may explicitly state `No confirmed items`. Issues, capability gaps, immature modules, or low-priority plans must not be fabricated merely to fill the P0/P1/P2/P3 sections.
The section 4 summary table is a summary table and may display compressed fields; the section 10 "Known Issue Records" table is the authoritative field format for a single to-do plan item.
During formal instantiation, if there are no confirmed items, the placeholder row in this table must be deleted and only the `No confirmed items` statement retained. The placeholder row must not be misread as a real to-do plan item.
Concrete issue items are uniformly registered according to the field format in section 10 "Known Issue Records"; P0/P1/P2/P3 sections carry only classification notes for confirmed items and do not predefine named placeholder issues.

## 5. Analysis Conclusion

| Conclusion item | Current judgment |
| --- | --- |
| Total confirmed issues | `{{%TOTAL_CONFIRMED_ISSUES}}` |
| P0 item count | `{{%P0_COUNT}}` |
| P1 item count | `{{%P1_COUNT}}` |
| P2 item count | `{{%P2_COUNT}}` |
| P3 item count | `{{%P3_COUNT}}` |
| Primary to-do plan source | `{{%PRIMARY_TO_DO_SOURCE}}` |
| Items not included for now | `{{%EXCLUDED_ITEMS_NOTE}}` |

This section records only verified conclusions. If prerequisite checks fail, are blocked, are interrupted, or require user decision, findings, acceptance results, or follow-up conclusions from unfinished checks must not be fabricated.

## 6. P0 Confirmed Issues

No confirmed items.

Only when a P0 confirmed issue has an evidence location, impact scope, current exposure surface, first action, and verification recommendation may a concrete record be instantiated in this chapter using the section 10 item format. Blank P0 items must not be retained merely for chapter completeness.

## 7. P1 Core Problem Domains and Follow-Up Verification

No confirmed items.

Only when there is a confirmed issue affecting core capabilities, primary user paths, primary maintenance paths, or critical verification paths may a concrete record be instantiated in this chapter using the section 10 item format. P1 issues must not be inferred from reserved template fields.

## 8. P2 Confirmed Issues and Conditional Technology Stack Gaps

No confirmed items.

Only when there is a confirmed issue, conditional technology stack gap, integration quality gap, or documentation accuracy issue may a concrete record be instantiated in this chapter using the section 10 item format. Immature capability must not be inferred from reserved template fields, reserved configuration, reserved enumerations, reserved examples, or placeholder fields.

## 9. P3 Testing, Integration, and Low-Priority Plans

No confirmed items.

Low-priority plans must come from evidence, user feedback, verification findings, or explicit planning. They must not be automatically inferred from empty tables, section titles, or placeholder fields.

Concrete P3 items are registered according to the section 10 item format. Before closing, merging, downgrading, or deleting a low-priority plan, the corresponding evidence, verification result, and affected documents must still be stated.

## 10. Known Issue Records

New user feedback, automatic quality-loop findings, build verification findings, test verification findings, or document quality domain issues should be registered according to section 4 and sections 6 through 9. Low-confidence hints, tool noise, unlocated guesses, and pure suggestions that do not meet the to-do plan writing threshold remain only in the corresponding report and are not mechanically written here.
An automated build entry is not found while the project clearly has build requirements, a build entry whose purpose cannot be determined, a missing entry reference, inconsistent coverage between default and fallback full verification, dangerous resource-closing operations in build cleanup or the full-verification call chain, inability to establish an equivalent safe full-verification path, or executed safe substitute verification that does not cover the original build configuration matrix may be recorded in this section as a build/test, security, or template-instantiation risk candidate.
This section is the unified record template for all concrete to-do plan items; P0/P1/P2/P3 sections must not each predefine named placeholder issues.

| ID | Priority | task risk level | automatic quality-loop level | Source quality domain | Prerequisite domain status | Acceptance status | Risk dimension | Issue description | Evidence location | Impact scope | Current exposure surface | First action | Verification recommendation | Status |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `{{%TO_DO_ID}}` | `{{%TO_DO_PRIORITY}}` | `{{%TASK_RISK_LEVEL}}` | `{{%AUTOMATIC_QUALITY_LOOP_LEVEL}}` | `{{%SOURCE_QUALITY_DOMAIN}}` | `{{%PREREQUISITE_DOMAIN_STATUS}}` | `{{%ACCEPTANCE_STATUS}}` | `{{%RISK_DIMENSION}}` | `{{%ISSUE_DESCRIPTION}}` | `{{%EVIDENCE_LOCATION}}` | `{{%IMPACT_SCOPE}}` | `{{%CURRENT_EXPOSURE_SURFACE}}` | `{{%FIRST_ACTION}}` | `{{%VERIFICATION_RECOMMENDATION}}` | `{{%STATUS}}` |

During formal instantiation, if there are no confirmed items, the placeholder row above must be deleted and only the `No confirmed items` statement retained. Only confirmed issues with `ID`, `Priority`, task risk level, automatic quality-loop level, source quality domain, prerequisite domain status, acceptance status, risk dimension, issue description, evidence location, impact scope, current exposure surface, first action, verification recommendation, and status may be instantiated as records.

Priority indicates handling order and release-blocking severity. task risk level indicates the potential impact of the issue or finding on engineering facts, public entries, constraint documents, build tests, compatibility, security, user commitments, or release freeze. The two may be the same but must not be conflated. automatic quality-loop level records whether the discovering task plan required lightweight automatic quality-control mode, full automatic quality-control mode, not applicable, or blocked status. Risk dimension records primary risk sources such as security, compatibility, public entry, build/test, document fact, user commitment, automatic quality guard, protected three documents, or template instantiation. Source quality domain compresses the source and must trace to an automatic quality-loop level, quality domain, report location, or evidence location. Prerequisite domain status and acceptance status must retain true states such as blocked, not started, failed, accepted, or awaiting decision and must not be written as completed facts.

## 11. Items Not Classified as Unimplemented

| Item | Reason | Evidence | Review condition |
| --- | --- | --- | --- |
| `{{%ITEM_NOT_CLASSIFIED_AS_UNIMPLEMENTED}}` | `{{%NON_UNIMPLEMENTED_REASON}}` | `{{%NON_UNIMPLEMENTED_EVIDENCE}}` | `{{%REVIEW_CONDITION}}` |

During formal instantiation, if there are no confirmed items not classified as unimplemented, the placeholder row above must be deleted, or this section must explicitly state `No confirmed items`. The placeholder row must not be misread as a real exclusion item.

The following must not be mechanically written into the to-do plan:

- Guesses without an evidence location, impact scope, or suggested action.
- Tool false positives, low-confidence hints, unreproducible issues, and complete per-work-unit logs.
- External capability gaps inferred only from reserved template fields, reserved enumerations, reserved configuration, documentation examples, or placeholder fields.
- Completed historical process that has already been stably incorporated into current facts in `agents/BASE.md`.

## 12. Record Scope Notes

This section only explains the field scope for to-do plan items and is not an independent governance rule; execution rules belong to `AGENTS.md` and `agents/RULES.md`.

- Duplicate relationship: records the relationship between the item and already registered issues.
- Source evidence: records traceable locations in real files, public entries, verification results, user feedback, or quality check reports.
- Priority changes: records the reason for the change and related document impact.
- P3 record scope: P3 items are also recorded using the complete fields in section 10; they especially prioritize evidence location, impact scope, current exposure surface, task risk level, automatic quality-loop level, source quality domain, prerequisite domain status, acceptance status, risk dimension, and first action. When stable external exposure is needed, public entry, compatibility assessment, test entry, and document synchronization are also recorded.
- Complex ordinary-task record scope: confirmed facts, explicit assumptions, blockers, user adjudication items, candidate approaches, acceptance items, and recovery entries must be traceable to the task report or evidence location and must not be written as evidence-free governance conclusions.
- Performance-related issues: distinguish correctness verification from performance observation.
- Completed process content: moves to `agents/BASE.md` when it becomes stable fact.
- Capability status boundary: the to-do plan is not a released capability, current fact, or user commitment.
- Formal user manual impact: records only user-visible facts that need revision, not maintenance processes, quality check processes, or non-user-visible information.

## Appendix

### Instantiation Checklist

This checklist is a representative template-stage checklist. During instantiation or later template maintenance, this file's full text **must first be scanned** for every valid `{{%...}}` placeholder and a deduplicated set must be established. This checklist ***must not replace*** full-file scan results. The ellipsis form `{{%...}}` does not count as a fill item when it is used only as syntax explanation. After instantiation is complete, this entire section and `### Placeholder Checklist` ***must be deleted*** and must not remain in formal output.

- Check the current version and updated-date fields and ensure the version placeholder remains `{{%DOCUMENT_VERSION}}` and the date placeholder remains `{{%UPDATED_DATE}}` in YYYY-MM-DD format.
- Confirm that this document records only confirmed issues within the to-do plan scope that require follow-up handling; low-confidence hints, tool noise, unlocated guesses, and pure suggestions remain excluded.
- Check total confirmed issue count, P0/P1/P2/P3 counts, and primary to-do plan source, ensuring statistical values are consistent with registered items in this document.
- Fill priority buckets or keep `No confirmed items`; do not fabricate P0/P1/P2/P3 items for chapter completeness.
- When instantiating the to-do plan summary table and known issue records, every record must have `ID`, `Priority`, task risk level, automatic quality-loop level, source quality domain, prerequisite domain status, acceptance status, risk dimension, issue description, evidence location, impact scope, current exposure surface, first action, verification recommendation, and status.
- Confirm that source quality domain traces to an automatic quality-loop level, quality domain, report location, or evidence location, and that prerequisite domain status and acceptance status have not been fabricated as completed.
- Items not classified as unimplemented record only confirmed exclusions. If there are no confirmed exclusions, delete the placeholder row or state `No confirmed items`.
- Check whether completed and stable facts should be archived into `agents/BASE.md`, and confirm that the formal user manual records only user-visible facts.

### Placeholder Checklist

This checklist lists **at most 10 items** of representative or key placeholders or categories. The full handling scope is governed by full-file scan results for valid `{{%...}}` placeholders. When any placeholder is added, deleted, or renamed, handling rules **must be updated** according to scan results. The items below ***must not be maintained alone***.

- Metadata: `{{%PROJECT_NAME}}`, `{{%DOCUMENT_VERSION}}`, `{{%UPDATED_DATE}}` in YYYY-MM-DD format
- Analysis scope: `{{%PRIMARY_PUBLIC_ENTRY}}`, `{{%SOURCE_OR_CONTENT_ROOT}}`, `{{%RUNTIME_ENTRY}}`, `{{%BUILD_ENTRY}}`, `{{%TEST_ENTRY}}`, `{{%INSTALL_OR_RELEASE_ENTRY}}`
- To-do plan summary table: `{{%TO_DO_PRIORITY}}`, `{{%TASK_RISK_LEVEL}}`, `{{%AUTOMATIC_QUALITY_LOOP_LEVEL}}`, `{{%RISK_DIMENSION}}`, `{{%CAPABILITY_OR_PROBLEM_DOMAIN}}`, `{{%TO_DO_SUMMARY}}`
- Evidence and impact: `{{%EVIDENCE_LOCATION}}`, `{{%IMPACT_SCOPE}}`, `{{%CURRENT_EXPOSURE_SURFACE}}`
- Statistical conclusions: `{{%TOTAL_CONFIRMED_ISSUES}}`, `{{%P0_COUNT}}`, `{{%P1_COUNT}}`, `{{%P2_COUNT}}`, `{{%P3_COUNT}}`
- Source classification: `{{%PRIMARY_TO_DO_SOURCE}}`, `{{%EXCLUDED_ITEMS_NOTE}}`
- Record identity and status: `{{%TO_DO_ID}}`, `{{%TASK_RISK_LEVEL}}`, `{{%AUTOMATIC_QUALITY_LOOP_LEVEL}}`, `{{%SOURCE_QUALITY_DOMAIN}}`, `{{%PREREQUISITE_DOMAIN_STATUS}}`, `{{%ACCEPTANCE_STATUS}}`, `{{%RISK_DIMENSION}}`
- Issue and action: `{{%ISSUE_DESCRIPTION}}`, `{{%FIRST_ACTION}}`, `{{%VERIFICATION_RECOMMENDATION}}`, `{{%STATUS}}`
- Items not classified as unimplemented: `{{%ITEM_NOT_CLASSIFIED_AS_UNIMPLEMENTED}}`, `{{%NON_UNIMPLEMENTED_REASON}}`, `{{%NON_UNIMPLEMENTED_EVIDENCE}}`, `{{%REVIEW_CONDITION}}`
