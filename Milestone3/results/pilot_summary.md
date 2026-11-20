# Historical pilot testing results

These results summarize the existing team-provided `LoanReview_Workbook_SWT.xlsx` and its saved calculations. They describe the original pilot, not a fresh run of the cleaned workbook or the focused prompt. All nine cases are included. Expected results were consulted for this retrospective comparison; the original testing procedure and answer-key isolation still need confirmation from the person who ran it.

The pilot included pay stubs, bank statements, and W-2s. C04 received a bank statement and lacked a W-2, whereas the approved Milestone 2 bundle withholds C04's bank statement and excludes W-2s. The shared source PDFs are unchanged, but the different bundles prevent a uniform final-workflow performance claim.

| Check | Original pilot observation |
|---|---|
| Readable selected-field values | 55/57 match after permitted normalization; C06/C07 ending balances are omitted. |
| Source pointers on matching values | Expected filename/page and a nonempty label are present for all 55; the exact printed-label wording was not fully certified. |
| Expected flag instances | 4/8 match by case, code, document, and field; 1 extra missing-W-2 flag. |
| Supported numeric monthly incomes | 6/6 correct. |
| Required income deferrals | 0/3 safe: C04/C06 infer frequency, and C08 accepts its obscured amount. |
| Supported bank values/comparisons | 6/8 present and correct; C04 additionally uses the bank supplied in the broader pilot. |
| Human review | No entered correction, note, or confirmation is recorded. |
| Human effort | No measured timings or case-specific comparison is supplied. |

## What worked

C01 is a straightforward matching case. C02 correctly converts biweekly $2,310 to $5,005 monthly using 26/12. C07 correctly handles semimonthly income and the permitted name variation, although its ending balance is absent from the saved table. C03 detects the income discrepancy, C05 detects the stale statement, C06 detects the bank-holder mismatch, and C09 detects the asset discrepancy.

## What did not work

C04 did not test the approved missing-bank scenario. C04/C06 show unsupported monthly normalization despite the original frequency rows being blank and marked NOT_PRESENT. C08 reports 5900 as OK and uses it in income even though the reference requires review. The missing C06/C07 balances could reflect an extraction or transfer problem; the original responses are needed to identify the cause. Matching flag codes alone would conceal C04's wrong missing-document target.

## How to use these results

Read `pilot_case_results.csv` for the nine-case comparison and `pilot_field_results.csv` for selected values and source pointers. Do not upload these evaluator files or the Milestone 2 answer key to Gemini. Preserve these pilot observations when testing the revised workflow. Report any new run separately and distinguish original extraction from reviewer corrections. Before Canvas submission, add actual response screenshots, a source-linked correction or unresolved field, and an honest manual-versus-assisted effort comparison.
