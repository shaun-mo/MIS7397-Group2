# Verification rules

These are **fictional class-scenario rules**, not industry, regulatory, tax, or lending guidance. Give this generic document to the prototype with one application row and its supplied pay-stub/bank-statement PDFs. Do not provide evaluator answers.

## Seven selected extraction fields

| Document | Fields |
|---|---|
| Pay stub | `employee_name`, `pay_date`, `pay_frequency`, `gross_pay_current_period` |
| Bank statement | `account_holder`, `statement_period_end`, `ending_balance` |

Every selected field needs its source filename, page, and printed label/region for human checking. Gross pay is the current-period amount, not net, YTD, or prior-year wages. The bank amount is the statement's ending balance. Other visible fields are outside the scored extraction scope.

Use numbers for USD amounts, ISO `YYYY-MM-DD` dates, and `monthly`, `biweekly`, or `semimonthly` for a printed frequency. A missing whole required document has status `NOT_SUBMITTED` and no fabricated fields. A required field not stated in a submitted document has value `null` and status `NOT_STATED`. A smudged/unreliable field has trusted value `null` and status `REVIEW_REQUIRED`. Usable fields have status `READABLE`; that is not human approval for decision use.

Do not infer recurring pay frequency from a single pay-period window. Do not replace an unsupported field with application-stated values, YTD/W-2 arithmetic, or back-calculation from other amounts. A visibly smudged or obscured target field requires review even if tentative digits can be read. Image-only format, skew, or background noise alone does not require a flag when the field remains reliably legible. A tentative candidate may be shown separately only with an explicit unverified warning; it must not enter trusted fields or verified comparisons.

## Calculations and thresholds

Monthly-equivalent gross = current gross multiplied by **1** for monthly, **2** for semimonthly, or **26/12** for biweekly pay. Both gross and printed frequency must be usable; otherwise monthly income and the income comparison are `UNVERIFIED`. Round monthly income to cents with decimal half-up rounding before comparison.

For a positive documented amount:

`percentage difference = 100 x (application-stated amount - documented amount) / abs(documented amount)`

Use the unrounded difference to test the threshold; round only its displayed percentage to two decimals. Exactly 2% does not trigger a mismatch; strictly more than 2% does. A missing bank statement makes its balance comparison `UNVERIFIED`, not a match and not an invented asset discrepancy.

If a denominator is zero/nonpositive, a date is invalid/future-dated, or evidence cannot support a comparison, return `UNVERIFIED` and route the relevant field for review. Those boundary conditions are conservatively defined but not covered by the current cases.

For this synthetic benchmark, compare personal names after ignoring case, punctuation, and middle names/initials, using first and last names. This simplified rule is not real identity verification.

## Flag contract

| Flag | Trigger | Human action |
|---|---|---|
| `INCOME_MISMATCH` | Absolute stated-versus-supported monthly gross difference is strictly greater than 2% | Review amounts/calculation and resolve the discrepancy |
| `ASSET_MISMATCH` | Stated checking balance is strictly more than 2% above the statement ending balance; lower stated amounts are not flagged by this class rule | Review amounts and determine acceptability/ownership |
| `MISSING_DOCUMENT` | A required pay stub or bank statement is absent from the supplied bundle | Request the document; do not populate its fields |
| `STALE_DOCUMENT` | Pay date or statement period end is more than 60 calendar days before application; exactly 60 is not stale | Request recent evidence |
| `NAME_MISMATCH` | Normalized first/last name differs from the applicant | Review the identity/account relationship; do not decide it automatically |
| `LOW_CONFIDENCE_FIELD` | A required field is not stated, cannot be read reliably, is visibly obscured, or cannot support a required comparison | Identify the field, use null/unverified appropriately, and request review; the code denotes workflow uncertainty, not a calibrated probability |

Identify flags by `(case_id, flag_code, document, field)`. For a missing whole document use `field="(entire document)"` and one missing-document flag, not one low-confidence flag per nonexistent field. A blocked income calculation does not need a duplicate flag when gross/frequency already identifies the cause.

Apply all checks independently. A mathematical match does not cancel a stale-document or name flag. Deposits are not required to equal gross pay. Tax-document, debt, unusual-deposit, and fraud checks are outside this prototype's scope.

## Review-sheet behavior

Show selected values beside their source and let the reviewer accept or correct each result. Nothing is decision-usable until the underwriter confirms it. Never approve/deny/recommend a credit decision, silently resolve conflicts, or write unconfirmed figures into a system of record. No flags means only that these defined checks found no discrepancy; normal review remains required.
