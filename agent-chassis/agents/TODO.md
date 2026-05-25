# {{%PROJECT_NAME}} Follow-Up Implementation Plan

## 1. Version Information

- Current version: `{{%DOCUMENT_VERSION}}`
- Updated: {{%UPDATED_DATE}}
- Synchronized documents: `README.md {{%DOCUMENT_VERSION}}`, `AGENTS.md {{%DOCUMENT_VERSION}}`, `agents/RULES.md {{%DOCUMENT_VERSION}}`, `agents/BASE.md {{%DOCUMENT_VERSION}}`, `agents/TODO.md {{%DOCUMENT_VERSION}}`, `doc/DOCUMENTATION.md {{%DOCUMENT_VERSION}}`
- Analysis scope: `{{%PRIMARY_PUBLIC_ENTRY}}`, `{{%SOURCE_OR_CONTENT_ROOT}}`, `{{%RUNTIME_ENTRY}}`, `{{%BUILD_ENTRY}}`, `{{%TEST_ENTRY}}`, `{{%INSTALL_OR_RELEASE_ENTRY}}`, `README.md`, `AGENTS.md`, `agents/RULES.md`, `agents/BASE.md`, `doc/DOCUMENTATION.md`

## 2. Document Role

`agents/TODO.md` is the follow-up implementation plan and known issue record. It carries confirmed gaps, risks, priorities, evidence locations, impact scope, current exposure, first actions, and verification suggestions.

This document does not carry agent control rules, detailed engineering rules, automatic quality-guard orchestration, the full factual baseline, or formal user manual content. The agent control entry is governed by `AGENTS.md`; detailed engineering rules are governed by `agents/RULES.md`; project facts are governed by `agents/BASE.md`; the project entry is governed by `README.md`; the formal user manual is governed by `doc/DOCUMENTATION.md`.

## 3. Reading Guide

| Priority | Meaning | Handling rule |
| --- | --- | --- |
| P0 | Confirmed issue that blocks release, breaks compatibility, misleads user boundaries, creates security risk, or makes a core flow unusable. | Handle first; record evidence, impact scope, and verification results before and after the fix. |
| P1 | Confirmed issue affecting core capabilities, primary user paths, primary maintenance paths, or critical verification paths. | Fill design, implementation, tests, and documentation synchronization as soon as possible. |
| P2 | Confirmed issue affecting secondary capabilities, conditional technology stacks, integration quality, or documentation accuracy. | Schedule for a later iteration, and confirm scope and compatibility before handling. |
| P3 | Confirmed low-priority plan, experience improvement, test enhancement, documentation supplement, or user-feedback suggestion. | Handle after requirements are clear, resources are available, or related modules are stable. |

Every confirmed TODO must have traceable evidence, impact scope, current exposure, first action, and verification suggestion. Low-confidence hints, tool noise, unlocated guesses, and broad risk notes should not be mechanically written here; they may remain in the corresponding report pending review.

## 4. TODO Summary Table

| Priority | Problem domain/module/item | Evidence location | TODO summary | Current exposure | First action |
| --- | --- | --- | --- | --- | --- |
| {{%TODO_PRIORITY}} | {{%CAPABILITY_OR_PROBLEM_DOMAIN}} | `{{%EVIDENCE_LOCATION}}` | {{%TODO_SUMMARY}} | {{%CURRENT_EXPOSURE}} | {{%FIRST_ACTION}} |

When there are no confirmed issues, this table may explicitly state `No confirmed items`. During formal instantiation, if there are no confirmed items, the placeholder row above must be deleted and only the `No confirmed items` statement retained. The placeholder row must not be misread as a real TODO.

Concrete issues are recorded using the field format in section 10, "Known Issue Records." P0/P1/P2/P3 sections carry classification notes only for confirmed items and do not predefine named placeholder issues.

## 5. Analysis Conclusion

| Conclusion item | Current judgment |
| --- | --- |
| Total confirmed issues | {{%TOTAL_CONFIRMED_ISSUES}} |
| P0 count | {{%P0_COUNT}} |
| P1 count | {{%P1_COUNT}} |
| P2 count | {{%P2_COUNT}} |
| P3 count | {{%P3_COUNT}} |
| Primary TODO source | {{%PRIMARY_TODO_SOURCE}} |
| Items not included in this round | {{%EXCLUDED_ITEMS_NOTE}} |

This section records verified conclusions only. If preceding checks fail, are blocked, are interrupted, or require user judgment, do not fabricate unfinished findings, acceptance results, or follow-up conclusions.

## 6. P0 Confirmed Issues

No confirmed items.

Only when a P0 confirmed issue has an evidence location, impact scope, current exposure, first action, and verification suggestion may a concrete record be instantiated in this chapter using the section 10 item format. Do not retain blank P0 items for structural completeness.

## 7. P1 Core Problem Domains and Follow-Up Verification

No confirmed items.

Only when a confirmed issue affects core capabilities, primary user paths, primary maintenance paths, or critical verification paths may a concrete record be instantiated in this chapter using the section 10 item format. Do not infer P1 issues from reserved template fields.

## 8. P2 Confirmed Issues and Conditional Technology-Stack Gaps

No confirmed items.

Only when there is a confirmed issue, conditional technology-stack gap, integration quality gap, or documentation accuracy issue may a concrete record be instantiated in this chapter using the section 10 item format. Do not infer immature capability from reserved template fields, reserved configuration, reserved enum values, reserved examples, or internal placeholders.

## 9. P3 Tests, Integration, and Low-Priority Plans

No confirmed items.

Low-priority plans must come from evidence, user feedback, verification findings, or explicit planning. They must not be automatically inferred from empty tables, section titles, or placeholder fields.

Suggested completion order:

1. First confirm whether the issue has an evidence location, impact scope, current exposure, and first action.
2. After confirming that it needs stable public exposure, fill public entries, compatibility assessment, test entries, and documentation synchronization.
3. For projects involving performance, real-time behavior, security, compatibility, or user commitments, correctness verification and performance observation must remain separate; performance observation cannot replace correctness criteria.

Concrete P3 items are recorded using the section 10 item format. Before closing, merging, downgrading, or deleting a low-priority plan, evidence, verification results, and affected documents must still be stated.

## 10. Known Issue Records

This section is the unified record template for concrete TODOs. New user feedback, quality-check findings, build verification findings, test verification findings, or document quality issues should be recorded through section 4 and sections 6 through 9. Low-confidence hints, tool noise, unlocated guesses, and pure suggestions that do not meet the TODO writing threshold remain only in the corresponding report and are not mechanically written here.

| ID | Priority | Source | Issue description | Evidence location | Current exposure | First action | Verification suggestion | Status |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| {{%TODO_ID}} | {{%TODO_PRIORITY}} | {{%SOURCE}} | {{%ISSUE_DESCRIPTION}} | `{{%EVIDENCE_LOCATION}}` | {{%CURRENT_EXPOSURE}} | {{%FIRST_ACTION}} | {{%VERIFICATION_SUGGESTION}} | {{%STATUS}} |

During formal instantiation, if there are no confirmed items, the placeholder row above must be deleted and only the `No confirmed items` statement retained. Only confirmed issues with evidence location, impact scope, current exposure, first action, and verification suggestion may be instantiated as records.

Before closing, merging, downgrading, or deleting a TODO, the corresponding evidence, verification result, and affected documents must be stated. Do not delete still-valid confirmed issues merely to keep the table short.

## 11. Items Not Classified as Unimplemented

| Item | Reason | Evidence | Review condition |
| --- | --- | --- | --- |
| {{%ITEM_NOT_CLASSIFIED_AS_UNIMPLEMENTED}} | {{%NON_UNIMPLEMENTED_REASON}} | `{{%NON_UNIMPLEMENTED_EVIDENCE}}` | {{%REVIEW_CONDITION}} |

The following must not be mechanically written as TODOs:

- Guesses without an evidence location, impact scope, or suggested action.
- Tool false positives, low-confidence hints, unreproducible issues, and complete per-work-unit logs.
- External capability gaps inferred only from reserved template fields, reserved enum values, reserved configuration, documentation examples, or internal placeholders.
- Completed historical process that has already become stable current fact in `agents/BASE.md`.

## 12. Maintenance Rules

- Before adding a TODO, confirm that it is not a duplicate of an existing item.
- The TODO source, evidence location, and current exposure must be traceable to real files, public entries, verification results, user feedback, or quality-check reports.
- Priority changes must state the reason and check whether related documents are affected.
- Completed process content is not retained long-term. If it becomes stable fact, move it to `agents/BASE.md`.
- TODOs must not be written as released capabilities, current facts, or user commitments.
- Impacts on the formal user manual record only user-visible facts that need revision; they do not record internal orchestration or maintenance flows.
