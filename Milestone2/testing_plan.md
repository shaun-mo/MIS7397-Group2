# Testing plan

## Procedure

In Milestone 3, run all nine cases through the focused pay-stub/bank-statement workflow. This milestone establishes inputs and references; **no prototype has been run and no performance result is claimed**.

1. Record the input/reference version, prompt/configuration, tool/model, and run date.
2. Supply only the matching application row, that case's available PDFs, and generic verification rules. Exclude this plan, README case descriptions, expected results, and private generation material from the prototype context.
3. Save the review sheet. Compare selected fields/statuses/source locations against `expected_extractions.json`, and complete flag instances against `expected_flags.csv`.
4. Log expected versus actual output, case/document/field or flag, correctness, severity, reviewer, and explanation. Count missing outputs as failures. Check that a reviewer can accept/correct each extracted figure before use.
5. Have a teammate resolve disputed references against the source. Separate answer-key corrections from model errors and identify rerun versions.

## Representative tests

| Case type | Actual inputs | Expected result | Incorrect behavior |
|---|---|---|---|
| Straightforward: C01 | C01 row, pay stub, bank statement | Monthly gross $5,400.00; selected values/sources correct; no flags; human acceptance required | Wrong value/source, omitted field, false flag, or automatic approval |
| Challenging layout: C02 | C02 row and two PDFs | Biweekly $2,310 x26/12 = $5,005 monthly; no flags | Using x2 and falsely comparing $4,620 with the application |
| Challenging names: C07 | C07 row and two PDFs | Semimonthly $3,150 x2 = $6,300; middle-initial/capitalization variants match | Name false positive or incorrect conversion |
| Missing document/field: C04 | C04 row and pay stub; bank statement intentionally withheld | Missing-bank flag plus frequency uncertainty; no bank fields; income/balance comparisons unverified | Fabricated balance/frequency, missing flag, or unsupported verified comparison |
| Concurrent issues: C06 | C06 row and two PDFs | Different bank holder flags name mismatch; unprinted frequency also flags uncertainty; income unverified | Catching only one issue or automatically resolving ownership/frequency |
| Degraded evidence: C08 | C08 row, scanned stub, bank statement | Smudged gross held for review; trusted gross/monthly income null; income unverified | Treating tentative digits or back-calculation as trusted extraction |

PDFs are in `sample_inputs/documents/`. Remaining cases: **C03** income mismatch ($7,500 vs $6,200, +20.97%); **C05** stale statement (112 days); **C09** asset mismatch ($15,000 vs $6,214.05, +141.39%). C08 may include an explicitly unverified tentative 5900.00 candidate, but its review gate must remain. W-2s are not required or checked in this core workflow.

## Scoring and error recognition

| Check | Rule |
|---|---|
| Readable-field accuracy | **57 fields**: 60 declared (36 pay-stub +24 bank) minus C04/C06 frequency and C08 review-required gross. C04's absent bank has no declared fields. Omitted/wrong eligible outputs are incorrect. |
| Value normalization | Normalize equivalent currency/date formatting and permitted name variants; compare amounts to the cent. Track formatting separately. Incorrect/ambiguous dates or amounts remain substantive errors. |
| Source correctness | Verify filename/page/label identifies the actual field. A correct value with the wrong source fails this check. |
| Derived income | Six numeric results: C01/C02/C03/C05/C07/C09. C04/C06/C08 remain null/`UNVERIFIED`. Score separately from the 57 extraction fields. |
| Balance comparisons | Eight numeric comparisons; C04 is `UNVERIFIED` because its statement is absent. Do not fill it from the application. |
| Complete flag sets | Match all `(case_id, code, document, field)` instances: eight across six flagged cases. Reject extras on flagged and clean cases. `NONE` means an empty set. |
| Safe review | Check required null/status, blocked calculations, human action, source presentation, and accept/correct behavior before use. |

**Critical errors:** unsupported/wrong financial value presented as trusted, missing required flag, fabricated missing-document fields, bypassed review, or credit-decision/automatic-resolution behavior. A wrong replacement flag can be both a missed expected instance and an extra flag. **Other errors:** false flags, wrong/omitted nonfinancial fields, source errors, and unnecessary abstentions. Equivalent display formatting is logged separately after normalization.

Targets are zero critical errors, all eight expected flags, zero unexpected flags across all cases, at least **55/57 readable fields correct** (the smallest integer meeting 95%), correct sources, six correct derived incomes, three safe income deferrals, and C04's safe balance deferral. These targets do not establish production reliability. C08's tentative candidate is excluded from normal readable-field scoring; its review behavior is checked separately.

## Comparison with the non-AI alternative

Use the **same nine cases, seven selected fields, source documents, expected flags, and human-review outputs** when explaining or measuring alternatives. A structured intake form captures applicant-stated values but still needs source verification; a checklist helps find missing/stale documents; a fixed template may extract familiar layouts but handle variation poorly. AI may assist with varying layouts while introducing misreads or unsupported assumptions. No winner is assumed in advance.

A conceptual comparison is sufficient for this milestone; a second full system is unnecessary. In Milestone 3, compare coverage and failure modes against the same answer key. Report measured improvements only if actually observed. A manual structured worksheet/checklist can be the non-AI reference process.

## Consistent timing definition

If timing is collected later, measure **human active review and data-entry minutes per case**: start when the reviewer begins the prepared case; stop when the seven selected fields and applicable flags are reviewed, accepted/corrected or explicitly unresolved, and recorded. Include active reading, checking, correction, and entry; exclude queue time, external handoffs/waiting, idle time, and model-processing waits. Record model runtime separately. Use the same pause rules and required outputs for both workflows.

The hypothetical Milestone 1 25-minute full-file baseline and under-10-minute target are **not measured results and are not directly comparable** to this narrower seven-field benchmark. Document-received-to-decision-ready elapsed time is a different metric and will not be substituted. No timing experiment is required for Milestone 2.

## Limits

Nine synthetic cases cover straightforward, challenging, missing, concurrent, and degraded evidence, but not the range of real documents or threshold boundaries. The prototype is limited to supplied layouts/fields. Tax returns/W-2 processing, debts, unusual deposits, fraud, production systems, and real applicant data remain outside scope.
