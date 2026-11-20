# AI-assisted loan document review

**Milestone 3 Implementation Report · MIS 7397 · Group 2**

Shaun Morris, Sarah Toups, and Tyler Drummond

## 1. Prototype Overview

A loan processor needs to trace an applicant’s stated income and checking balance to supporting documents. Our prototype uses Gemini to read four pay-stub fields (employee name, pay date, printed frequency, and current-period gross pay) and three bank-statement fields (account holder, statement period end, and ending balance). Excel compares those figures with the application and gives a person a place to record corrections or unresolved questions. The underwriter retains the lending decision.

## 2. Tools and Implementation Approach

Gemini can read PDFs with different layouts, including scanned pages. Excel makes the calculations visible and keeps the applicant’s claims separate from document values and reviewer changes. A person manually transfers the extraction table from Gemini to Excel. Each row includes a status and space for the filename, page, and printed label.

The nine-case pilot used a broader prompt and 26 documents, including eight W-2s and C04’s bank statement. We preserved all 158 pilot rows and narrowed the instructions and review fields to match the 17 published Milestone 2 PDFs. For a focused run, only the case PDFs go to Gemini. Answer-key isolation in the historical pilot still needs confirmation from the person who ran it. The focused instructions have yet to be tested in Gemini.

## 3. Evidence That the Prototype Works

The saved C02 extraction identifies $2,310 as current-period gross pay and biweekly as the printed frequency. Excel calculated $2,310 × 26 ÷ 12 = $5,005 monthly, matching the application. This example shows how a source value feeds a check that the reviewer can reproduce.

**Canvas figures still needed.** Include a screenshot of Gemini returning fields from an uploaded document and a second view showing a source alongside a real correction or unresolved hold in Excel. Caption each with the input, output, and finding. Identify new demonstrations separately from the pilot.

## 4. Testing Results

**55 of 57 readable values matched** the Milestone 2 reference. All six supported monthly incomes were correct. The original workbook also calculated income in all three cases that required deferral. Four of eight expected flags matched by case, code, document, and field. The pilot raised one extra flag for a missing W-2.

| Case | Original pilot outcome compared with Milestone 2 |
|---|---|
| C01 · straightforward | $5,400 monthly with no discrepancy flag, as expected. |
| C02 · biweekly pay | $5,005 monthly with no discrepancy flag, as expected. |
| C03 · income difference | Flagged $7,500 stated against $6,200 documented. |
| C04 · missing information | The pilot received the bank statement the published bundle withholds. Missing-bank behavior remains untested. It calculated $4,750 monthly despite no printed frequency. |
| C05 · document age | Flagged the bank statement dated 112 days before the application. |
| C06 · concurrent issues | Flagged the account-holder mismatch, missed the missing frequency, and calculated unsupported monthly income of $4,100. The ending-balance row was absent. |
| C07 · name and layout variations | Matched the name variation and converted $3,150 semimonthly to $6,300 monthly. The ending-balance row was absent. |
| C08 · degraded scan | Recorded the obscured gross as $5,900 with status `OK` and used it as monthly income. The field required review. |
| C09 · asset difference | Flagged $15,000 stated against a $6,214.05 ending balance. |

## 5. Challenges and How We Addressed Them

The pilot inferred frequency from a single pay-period window. This made unsupported income look consistent with the application. We removed the inference and separated preliminary calculations from confirmed figures. The revised workbook lets the reviewer accept a value, correct it with a source note, or hold it. A genuine reviewer decision is still needed for the demonstration.

The missing C06 and C07 balances exposed a risk in manual transfer. The saved rows alone cannot identify whether the omission occurred in extraction or during the paste. Our runbook now calls for comparing the pasted rows with the original response before evaluation.

## 6. Current Limitations and Next Steps

Nine synthetic applications and one degraded scan give us a narrow test of the reading task. The different input bundles limit comparisons with the focused workflow. Before submitting, we need to demonstrate C04 using only its published pay stub and check C08’s obscured field against the scan. Running all nine cases under the focused instructions would support a comparable score for that version.

The pilot has no case-specific comparison of human effort. We still need to compare manual extraction with AI-assisted transfer and verification on the same case, seven fields, and flags. Any timed comparison should separate active human work from model waiting. Current results support no estimate of time savings.
