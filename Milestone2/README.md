# Milestone 2 - Prototype-Ready Evidence Package

**MIS 7397 | Group 2 | AI-assisted loan-document review**

**Due November 5, 2026 | 5% of course grade**

This package prepares a focused Milestone 3 demonstration: **two document types, seven selected fields, nine fictional applications, and 17 source PDFs**. The assistant will extract selected pay-stub and bank-statement fields, compare supported figures with the application, and show sources and flags for a person to accept or correct. It will not make lending decisions. No working application or prototype performance result is claimed here.

## Package contents

| Location | Purpose |
|---|---|
| [sample_inputs/applications.csv](sample_inputs/applications.csv) | Nine application rows: stated monthly income/checking balance and the documents actually supplied for each test |
| [sample_inputs/documents/](sample_inputs/documents/) | Nine pay stubs and eight bank statements; C04's statement is deliberately withheld for the missing-document test |
| [reference/verification_rules.md](reference/verification_rules.md) | Generic fields, normalization, comparison rules, and review behavior given to the prototype |
| [expected_results/expected_extractions.json](expected_results/expected_extractions.json) | Evaluator-only values, field statuses, sources, derived income, and comparison outcomes |
| [expected_results/expected_flags.csv](expected_results/expected_flags.csv) | Evaluator-only flag instances, supporting locations, reasons, and human actions |
| [expected_results/case_index.csv](expected_results/case_index.csv) | Evaluator-only case overview and expected outcomes |
| [testing_plan.md](testing_plan.md) | Cases, scoring, failure recognition, and comparison with the non-AI alternative |
| [scope.md](scope.md) | Implementation boundaries and response to Milestone 1 feedback |

## Use and evaluation separation

For each run, give the prototype **only the matching application row, that case's supplied PDFs, and the generic verification rules**. Exclude this README's case descriptions, `expected_results/`, and the testing plan: they contain answers. Private generation material must also stay outside its context.

The review sheet will show each selected value with its source filename/page/label and allow a human to accept or correct it. Unsupported fields and dependent comparisons remain unverified. A mathematical match means consistency under the class rules, not acceptable evidence, account ownership, decision readiness, or loan eligibility. All figures need human confirmation before decision use.

## Case coverage

All applications are dated **October 20, 2026**; amounts are USD. Extra information visible in the PDFs is outside the seven scored extraction fields.

| Case | Behavior tested | Expected flags |
|---|---|---|
| C01 | Clear documents and monthly pay | None |
| C02 | Different layout; biweekly gross converted with 26/12 | None |
| C03 | Stated monthly income exceeds supported monthly income | `INCOME_MISMATCH` |
| C04 | Bank statement withheld; pay frequency not printed | `MISSING_DOCUMENT`; `LOW_CONFIDENCE_FIELD` on frequency |
| C05 | Bank statement predates the application by 112 days | `STALE_DOCUMENT` |
| C06 | Different bank-account holder; pay frequency not printed | `NAME_MISMATCH`; `LOW_CONFIDENCE_FIELD` on frequency |
| C07 | Name-format variations and semimonthly pay | None |
| C08 | Smudged gross field in an image-only scan | `LOW_CONFIDENCE_FIELD` on gross |
| C09 | Stated checking balance exceeds the statement balance | `ASSET_MISMATCH` |

There are eight expected flag instances across six cases and three no-flag cases. C04/C06/C08 monthly income is unverified. C04's balance comparison is also unverified because its statement is absent. C08's digits may be tentatively readable; the case tests the smudged-field review policy rather than an absolute inability to read the image.

## Provenance and preparation

The supplied package identifies its people, employers, banks, and figures as fictional/synthetic and discloses Claude assistance in generating source documents and initial answers. PDFs carry a fictional-data footer. This benchmark is not real applicant data or lending guidance.

The 17 included PDFs are unchanged source copies. To implement the instructor's focused-scope feedback, W-2s were excluded and C04's bank statement was intentionally withheld. The application CSV is a **reviewed derivative**: only `documents_submitted` was adjusted to reflect the two-type bundle and C04's deliberate omission. All other application columns and values remain unchanged. The complete original package is preserved privately.

Codex and Astra reviewed all original document pages and source/reference arithmetic, then refined the selected-field references, uncertainty rules, and testing instructions. This is reference-package verification, not a prototype run. Common-source synthetic generation and nine cases cannot establish real-world reliability.

Milestone 1 feedback is addressed in the scope and testing plan. The team is Shaun Morris, Tyler Drummond, and Sarah Toups. This is synthetic class data; no external dataset-author citation or separate team sign-off is required. Keep actual member contributions identifiable through GitHub commits/reviews where possible, as the assignment requests. AI assistance is disclosed above.
