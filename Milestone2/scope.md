# Initial prototype scope

## Focused implementation

Build a demonstration for one synthetic application at a time using **two document types and seven fields**:

- Pay stub: employee name, pay date, printed pay frequency, current-period gross pay.
- Bank statement: account holder, statement period end, ending balance.

The assistant will extract those fields with source filename/page/label, calculate monthly gross only when supported, compare income/checking balance with the application, and identify the six flag categories in [verification_rules.md](reference/verification_rules.md). The review sheet will let a person **accept or correct each result**. All values require underwriter confirmation before use; the assistant does not make lending decisions.

The set contains nine application rows and 17 PDFs. C04's bank statement is deliberately withheld to test a missing required document; its application row reflects that bundle. W-2s and unused original documents are deferred rather than required inputs. Extra fields visible in PDFs are outside the seven-field scoring contract.

Implementation will use the environment permitted by the next assignment and course-approved UH-managed accounts. No production systems or third-party connectors are required. A configured tool/application is not a Milestone 2 deliverable; this package prepares evidence for that later work.

## Response to Milestone 1 feedback

| Instructor improvement | Response |
|---|---|
| Align manual-review timing with its measurement | Define human active review/data-entry minutes on identical cases/fields; distinguish model runtime and elapsed cycle time. Do not reuse the hypothetical full-file baseline as a measured seven-field result. |
| Prepare fictional documents with known values, uncertainty, and intentional mismatches | Supply nine cases with verified references, income/asset mismatches, missing statement/frequency, and a smudged-field review case. |
| Start with one or two document types and a few fields | Limit core work to pay stubs and bank statements, four plus three fields; defer W-2s, tax returns, debts, and wider extraction. |
| Keep the non-AI comparison simple | Compare identical cases/outputs with structured intake, checklist, or template methods conceptually; no second system or unmeasured improvement claim. |

The feedback approved investigating the Milestone 1 idea. It is not instructor approval of Milestone 2 or this specific implementation. These changes respond to the feedback while preserving human confirmation.

## Boundaries and evaluation

Use [testing_plan.md](testing_plan.md) to evaluate selected-field/source accuracy, expected and unexpected flags, safe deferral, and reviewer accept/correct behavior. Keep evaluator answers out of prototype context. No functioning prototype or observed performance is claimed here.

Outside scope: autonomous credit decisions/recommendations, broad fraud/tampering detection, joint-account acceptance decisions, tax-document processing, debts, unusual deposits, multiple-account/month reconciliation, LOS integration, real borrower data, and production reliability claims. A human resolves conflicts and decides evidence acceptability.

This is the defined initial implementation scope for the evidence package. If implementation choices change, update the rules, examples, and expected results together before evaluation. No separate team sign-off document is required by the milestone.
