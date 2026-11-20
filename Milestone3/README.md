# Milestone 3 · AI-assisted loan document review

**MIS 7397 · Group 2 · Shaun Morris, Sarah Toups, and Tyler Drummond**

A loan reviewer needs to trace an applicant’s stated income and checking balance back to supporting documents. Our prototype uses Gemini to read a pay stub and bank statement. A person transfers the extraction table into Excel, checks each value against its source, and records corrections or holds. Excel applies the same income, balance, age, and name checks across cases. Lending decisions stay with the underwriter.

## Review the prototype

Read the [six-section implementation report](Implementation_Report.md) for the business problem, case outcomes, and limitations. The Canvas copy still needs screenshots of the working prototype and a comparison of human effort.

| Start here | What to look for |
|---|---|
| [Loan review workbook](LoanReview_Workbook.xlsx) | Open `AI_Raw` for the 158 original pilot rows, `Review` for source checks, and `Checks` for the revised spreadsheet calculations. |
| [Pilot results](results/pilot_summary.md) | The original nine-case results, including which fields matched, which flags appeared, and where the workflow accepted unsupported income. See the [case comparisons](results/pilot_case_results.csv) and [field comparisons](results/pilot_field_results.csv). |
| [Milestone 2 inputs](../Milestone2/sample_inputs/documents/) | The focused demonstration uses 17 fictional PDFs. The [application rows](../Milestone2/sample_inputs/applications.csv) supply the figures Excel compares. The [verification rules](../Milestone2/reference/verification_rules.md) define the seven fields, calculations, and review conditions. |
| [Runbook](RUNBOOK.md) and [extraction instructions](gemini_extraction_instructions.md) | Use a copy of the workbook for a new run. The runbook covers input selection, manual transfer, review, and comparison with the answer key after extraction. |

## What the pilot showed

The pilot covered nine fictional applications and used a broader set of documents. It included eight W-2s and a bank statement for C04. The focused workflow reads four pay-stub fields and three bank-statement fields. Its C04 bundle contains only the pay stub.

Against the Milestone 2 reference, **55 of 57 readable values matched**. C06 and C07 had no ending-balance row. The original workbook calculated all six supported monthly incomes correctly, but it also calculated income in all three cases that required a hold. Four of eight expected flag instances matched. These are retrospective results from the original pilot. The revised workbook preserves those inputs, and its current checks can differ from the recorded pilot results.

## Before the Canvas report is submitted

- [ ] Use the published C04 bundle and C08 scan to demonstrate the missing statement and the obscured gross pay. Save actual output and show how the reviewer handles the result.
- [ ] In the Canvas report, include screenshots of Gemini returning fields and Excel showing a real correction or unresolved field. Caption each with the input, output, and finding. Include a straightforward and a challenging case in the results.
- [ ] Compare the human work of manual extraction with verifying an AI extraction on the same case and seven fields. Record what was observed and identify any measured time separately from model waiting.
