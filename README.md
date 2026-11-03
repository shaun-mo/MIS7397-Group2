# AI-Assisted Loan Document Extraction — Group 2

**MIS 7397 · Introduction to Artificial Intelligence for Business**
University of Houston, Bauer College of Business · Fall 2026 · Section 27425

This is the shared team repository for Group 2's semester capstone: an **AI Opportunity-to-Deployment** project that runs from opportunity proposal (Milestone 1) through prototype, feasibility analysis, governance plan, and final executive pitch.

---

## Team

| Member | GitHub | School Email |
|---|---|---|
| **Shaun Morris** | [@shaun-mo](https://github.com/shaun-mo) | sbmorri2@cougarnet.uh.edu |
| **Tyler Drummond** | [@tdrummond91](https://github.com/tdrummond91) | tsdrummo@CougarNet.UH.EDU |
| **Sarah Toups** | [@sarahtoups](https://github.com/sarahtoups) | scepeda4@CougarNet.UH.EDU |

All three members have write access to this repository.

---

## Business problem

Loan underwriters spend a large share of every file manually re-keying figures from applicant financial documents (pay stubs, bank statements, W-2s and tax forms) into the loan origination system, then cross-checking those figures against what the applicant stated on the application. The work is repetitive, error-prone, and a direct driver of underwriting cycle time. It happens on every file, every day.

We are investigating whether **document-grounded data extraction plus inconsistency detection** can cut document review time from roughly 25 minutes per file to under 10, without letting the rework/error rate rise above its current level. The underwriter keeps the credit decision. AI would only surface extracted figures and flags for human confirmation.

**Recommendation: INVESTIGATE.** Full reasoning, baseline figures, evidence path, non-AI alternative, and risk controls are in the `/docs` evidence package below.

> All baseline numbers are hypothetical planning estimates for a fictional scenario. Any prototype will use synthetic or public documents only. No real applicant data.

---

## Repository organization

**Milestone 2:** The [prototype-ready evidence package](Milestone2/README.md) contains synthetic applications and source documents, expected outputs, verification rules, a testing plan, and the initial prototype scope for the November 5 milestone.

```
introduction-to-ai-team-2/
│
├── README.md                     ← this overview
├── Course-Reference.md           ← syllabus summary: schedule, grading, policies
│
├── docs/                         ← Milestone 1 evidence package
│   ├── 01_problem_stakeholder.md
│   ├── 02_current_workflow.md
│   ├── 03_baseline_kpi.md
│   ├── 04_ai_fit.md
│   ├── 05_evidence_data_path.md
│   ├── 06_non_ai_alternative.md
│   ├── 07_risk_control.md
│   ├── 08_recommendation.md
│   └── 09_executive_summary.pptx
│
└── Class Notes/                  ← one folder per week: lecture PDF + markdown outline
    ├── Wk 1 - Aug 27 26/
    ├── Wk 2 - Sep 3 26/
    ├── Wk 3 - Sep 10 26/
    └── Wk 4 - Sep 17 26/
```

### Milestone 1 evidence package — `/docs`

Each topic is a separate file so the project logic can be reviewed one piece at a time.

| File | What it answers |
|---|---|
| [01_problem_stakeholder.md](docs/01_problem_stakeholder.md) | What specific pain exists? Who experiences it? Why does it matter? |
| [02_current_workflow.md](docs/02_current_workflow.md) | What happens today? Where are the delays, errors, handoffs, and repeated work? |
| [03_baseline_kpi.md](docs/03_baseline_kpi.md) | Current performance and the measurable target that counts as improvement |
| [04_ai_fit.md](docs/04_ai_fit.md) | Which AI capability fits, why AI is appropriate, and what AI would *not* do |
| [05_evidence_data_path.md](docs/05_evidence_data_path.md) | Evidence needed: source, access, quality, privacy, constraints |
| [06_non_ai_alternative.md](docs/06_non_ai_alternative.md) | The simpler non-AI solution the AI proposal must outperform |
| [07_risk_control.md](docs/07_risk_control.md) | One meaningful failure and one concrete initial guardrail |
| [08_recommendation.md](docs/08_recommendation.md) | INVESTIGATE, REFRAME, or REJECT, and why |
| [09_executive_summary.pptx](docs/09_executive_summary.pptx) | One-slide summary for the 60-second approval conversation |

### Other folders and files

| Location | Description |
|---|---|
| [Class Notes/](Class%20Notes/) | Lecture PDFs with markdown outlines, one folder per week. Week 3 covers the Milestone 1 spec and data readiness scorecard; Week 4 covers supervised learning and Applied Lab 1. |
| [Course-Reference.md](Course-Reference.md) | Syllabus summary: course info, objectives, schedule, capstone checkpoints, grading, policies |
| `[Syllabus] Intro to AI.pdf` | Full course syllabus (source document) |
| `.env.local.example` | Template for local secrets. Copy to `.env.local`, which is gitignored. |

---

## Milestone 1 submission — due Thursday, September 17, 2026

Milestone 1 is an approval package with three parts:

1. **Team repository** — this repo, with the eight detailed documents in `/docs` and the README kept to a project overview.
2. **Executive summary** — one slide in `docs/09_executive_summary.pptx` that lets a leader understand the opportunity in about 60 seconds.
3. **Canvas proof, one per person** — each of the three team members individually submits their own screenshot showing they are logged in with access to this repository, plus this repo's URL:

   ```
   https://github.com/shaun-mo/introduction-to-ai-team-2
   ```

   Three students, three screenshots, same URL.

---

## Working in this repo

```bash
# One-time: get a copy on your machine
git clone https://github.com/shaun-mo/introduction-to-ai-team-2.git

# Every time you start work: get the latest changes
git pull

# After you make changes: save and share them
git add .
git commit -m "Describe what you changed"
git push
```

**Adding a new week of notes:** create `Class Notes/Wk N - <Mon D YY>/`, drop the lecture PDF in, and add a `Week-N-Notes.md` outline beside it.

**Data policy:** never commit datasets containing confidential, proprietary, or personally identifiable information. Use public, synthetic, or instructor-approved data only.
