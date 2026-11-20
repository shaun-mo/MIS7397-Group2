# Run the loan document review

Use the [workbook](LoanReview_Workbook.xlsx) and Excel to inspect the existing pilot. To run the focused workflow, use a UH-managed Gemini account and a **separate copy** of the workbook. All inputs in this exercise are fictional.

## 1. Prepare the case

1. Save a working copy of the workbook. For a fresh run, clear the contents of `AI_Raw!A2:I500` and `Review!J2:L64` in that copy. Keep the headers and formulas. Record the case ID, date, tool/model displayed, and instructions used.
2. Find the case in [applications.csv](../Milestone2/sample_inputs/applications.csv). Select only that case’s [published PDFs](../Milestone2/sample_inputs/documents/). Most cases have a pay stub and bank statement. C04 has only a pay stub. C08 uses `C08_pay_stub_scan.pdf` and its bank statement.
3. On `Application_Stated`, set column G for the case to the documents actually supplied, using identifiers such as `pay_stub;bank_statement` or `pay_stub`. Column I lists the published bundle for comparison. Application amounts belong on this sheet.

## 2. Extract and transfer

1. Start a separate Gemini conversation for each applicant. Attach the selected PDFs and use the [extraction instructions](gemini_extraction_instructions.md) with that case ID. Keep the application amounts, case descriptions, workbook, and evaluation files outside the conversation.
2. Keep the original response for comparison. Copy its **data rows** into the next empty row of `AI_Raw`, columns A–I. This transfer is manual. Check the case ID, column alignment, dates, and source filename against the response.
3. With both PDFs present, expect four pay-stub rows and three bank-statement rows. A missing document has one `(document)` row in its place. If a row is absent from the response, record the omission. If it was lost during transfer, correct the paste from the original response. Keep reruns distinguishable.

## 3. Check a value against its source

Open `Review`. For each selected field, open the named PDF at the listed page and locate the printed label. Compare the value and its legibility. Leave `AI_Raw` as originally transferred.

| Reviewer finding | What to enter on `Review` |
|---|---|
| The source supports the extracted value | Select `ACCEPT` in column L. |
| The source supports a different value | Enter the source-supported replacement in J, explain the correction and location in K, and select `CORRECT` in L. |
| The field is missing, obscured, or still unresolved | Explain what is missing or what document is needed in K and select `HOLD` in L. |
| The field has yet to be checked | Leave the reviewer action blank. It stays pending. |

On `Checks`, column D shows the case review status. Compare candidate monthly income (N) and ending balance (Q) with confirmed monthly income (K) and ending balance (X). A plausible number on a smudged pay stub still requires a source check. A hold on gross pay blocks its use for confirmed income. Missing printed frequency also blocks a monthly conversion. Keep the review open when evidence is insufficient. A human retains the lending decision.

## 4. Compare results and record effort

After the run, compare original values, statuses, and source locations with the [expected extractions](../Milestone2/expected_results/expected_extractions.json). Compare flags by case, code, document, and field using the [expected flags](../Milestone2/expected_results/expected_flags.csv). Check missing rows, blocked calculations, and any changes after human review. Keep original and reviewed outcomes separate. Use the [testing plan](../Milestone2/testing_plan.md) for denominators and case expectations.

For the practical-value comparison, select the same case and seven fields for both methods. In the manual pass, read the PDFs and record the values, flags, and unresolved items. In the assisted pass, include upload, transfer, source checking, correction, and recording. Use `Effort_Log` for observations. When timing, compare **active human minutes** with the same start and finish points. Record model wait separately. If experience with the first pass influenced the second, note the order.

For Canvas, capture actual inputs and returned fields from a straightforward, a challenging, and a missing-information or uncertainty case as needed to explain the demonstration. Show at least one real reviewer correction or unresolved field beside its source and workbook result. Add these screenshots and captions directly to the Canvas report.
