# Gemini extraction instructions

Use these instructions for the focused two-document workflow. The saved nine-case pilot used a broader prompt. To try the focused version, open a new conversation in UH-managed Gemini, replace `[CASE ID]`, and attach only the PDFs for that application. Give application-stated values to Excel and reserve the [reference results](../Milestone2/expected_results/) for evaluation after extraction.

```text
Read the attached financial documents for case [CASE ID]. Transcribe the selected fields so a loan reviewer can check each one against its source. Use only the files attached to this message. Leave calculations, comparisons, and lending decisions to the review team.

Use these document types and field identifiers exactly.

pay_stub
  employee_name
  pay_date
  pay_frequency
  gross_pay_current_period

bank_statement
  account_holder
  statement_period_end
  ending_balance

Return a tab-separated table with this column order:
case_id, document, field, value, status, source_file, page, printed_label, notes

For each supplied document, return one row for every selected field, including fields you cannot read. Copy the exact uploaded filename, the page number starting at 1, and the printed label or location of each field. Identify the current-period column for gross pay and the end of the period for the statement date. Preserve names and printed frequency wording. Express dates as YYYY-MM-DD and currency as a signed decimal number with two places, without a currency symbol or thousands separators.

Assign one status per field:
OK              The field is printed and clearly legible. Enter its value.
LOW_CONFIDENCE  The target is smudged, obscured, or otherwise unreliable. Leave value empty. If helpful, put tentative digits in notes and label them unverified.
UNREADABLE      The field is present but you cannot read it. Leave value empty and identify the region.
NOT_PRESENT     The document is present but omits this field. Leave value empty and describe where you checked.

If an entire required document type is absent, return one row for that document with field (document), status NOT_PROVIDED, and notes explaining what was missing. Leave value, source_file, page, and printed_label empty for that row. Do not create individual field rows for the absent document.

Read pay frequency only when printed. Never derive it from pay dates or period length. Do not calculate current gross from net pay, year-to-date totals, or other fields. If a printed figure is obscured, require review even when a tentative reading looks plausible.

Output only the header and data rows, using tabs between columns. Preserve empty cells, including an empty notes cell when no explanation is needed.
```
