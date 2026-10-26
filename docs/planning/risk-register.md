# Risk Assessment & Mitigation Plan

| Item | Detail |
|---|---|
| Project | Customer Churn Intelligence & Retention System |
| Document owner | Business Analyst (بثينه), reviewed by the MLOps Engineer (مصطفى) |
| Version | 1.0 |
| Review cadence | Every weekly team sync |

---

## 1. Scoring Method

**Score = Likelihood x Impact**, each rated from 1 (lowest) to 5 (highest).

| Rating | Likelihood | Impact |
|---|---|---|
| 1 | Very unlikely | Negligible effect |
| 2 | Unlikely | Minor rework |
| 3 | Possible | Delays a deliverable by days |
| 4 | Likely | Threatens a milestone |
| 5 | Almost certain | Threatens the project outcome |

| Score | Level | Response |
|---|---|---|
| 1 to 4 | Low | Monitor |
| 5 to 9 | Medium | Mitigate and review monthly |
| 10 to 15 | High | Active mitigation, review weekly |
| 16 to 25 | Critical | Immediate action, escalate to the project lead |

---

## 2. Risk Register

| ID | Risk | Category | L | I | Score | Level | Mitigation (prevent) | Contingency (if it happens) | Owner |
|---|---|---|---|---|---|---|---|---|---|
| R01 | Schedule pressure: planning documents are already late and the Design deliverable is due 6 Nov | Schedule | 4 | 4 | 16 | Critical | One owner per deliverable (see `task-assignment.md`); work in parallel; Must requirements first; progress check at every sync | Ask the lecturer for an extension; reduce diagram detail but keep every required item | Project lead, بثينه |
| R02 | Scope creep: MLOps extensions (MLflow, FastAPI, Docker, CI) take time from the core deliverables | Scope | 4 | 4 | 16 | Critical | Core first, extensions are Should; implementation freeze on 27 Nov; scope check each week | Drop deployment to the cloud and keep local Docker; drop SHAP | Project lead, مصطفى |
| R03 | Dataset limits: the Telco data is one flat table without dates and has no transaction or support data | Data | 5 | 3 | 15 | High | Generate synthetic tables and document them; show trends by tenure group; state limitations in the report | Reduce the SQL analysis on synthetic tables to what the data supports | عبدالله |
| R04 | Synthetic data is mistaken for real evidence, which weakens credibility | Data | 3 | 4 | 12 | High | Mark synthetic tables and fields in the data dictionary; no business conclusion from synthetic fields alone; limitations section in the report | Re-label results and remove claims based on synthetic fields | عبدالله, بثينه |
| R05 | Team availability: exams and other courses reduce capacity | Resources | 4 | 3 | 12 | High | Backup member for every role; buffer days before milestones; frequent small commits so work can be taken over | Backup member takes over; reduce optional items | Project lead |
| R06 | Unclear lecturer expectations and grading criteria (for example the meaning of the Literature Review section) | Requirements | 4 | 3 | 12 | High | Ask the lecturer in writing; keep documents aligned with the Guidelines headings; keep both interpretations covered | Adjust documents once the criteria arrive | بثينه |
| R07 | Data leakage or evaluation errors make results look better than they are | Quality | 3 | 4 | 12 | High | Split first; fit preprocessing on training data only (FR-12); reviewer checks the notebook; use pipelines | Re-run the evaluation and correct the report | محمد, مريم |
| R08 | Integration fails between model, API and dashboard | Technical | 3 | 4 | 12 | High | Agree the API contract early (FR-44); shared feature schema; serialize the full preprocessing pipeline; integration test by 20 Nov | Dashboard reads pre-scored predictions from a file instead of calling the API | مصطفى |
| R09 | Heavy design documentation load is unevenly shared | Schedule | 3 | 3 | 9 | Medium | Diagram owners assigned per person; shared templates; peer review on 5 Nov | Backup member takes over diagrams | Project lead |
| R10 | Model Recall stays below the target (provisional 0.70) | Technical | 3 | 3 | 9 | Medium | Class weights, threshold tuning, extra models (Random Forest, XGBoost), feature engineering; early baseline | Document the best result honestly with next steps, as required by FR-38 | محمد |
| R11 | Deployment problems (Docker build, versions, Hugging Face limits) | Technical | 3 | 3 | 9 | Medium | Local Docker is the minimum; pinned dependencies; test deployment early | Run locally and record a demo video | مصطفى |
| R12 | Git collaboration problems: merge conflicts, large files, lost work | Process | 3 | 3 | 9 | Medium | Feature branches and pull requests; `.gitignore` for data and model files; small commits | Restore from history; resolve conflicts in a team session | مصطفى |
| R13 | Environment differences ("works on my machine") | Technical | 3 | 3 | 9 | Medium | Pinned `requirements.txt`; same Python version; Docker; another member runs the README from scratch | Fix the setup instructions and re-test | مصطفى |
| R14 | Dashboard is hard to use or finished late | Quality | 3 | 3 | 9 | Medium | Wireframes approved early; loading, no-data and error states (FR-43); test with 3 people outside the team | Simplify the dashboard to the Must requirements | بسمله |
| R15 | Documents become inconsistent with each other (plan, requirements, design, tests) | Quality | 3 | 3 | 9 | Medium | Use requirement IDs everywhere; traceability table; cross-review before each milestone | Correct the documents before submission | بثينه |
| R16 | Explanations are over-interpreted as causes of churn | Ethics | 2 | 3 | 6 | Medium | Wording rules (NFR-23); business analyst reviews the report; no causal claims in recommendations (FR-40) | Reword the dashboard and report | بثينه |
| R17 | Secrets or real personal data are committed to the repository | Security | 2 | 4 | 8 | Medium | Public dataset only; `.gitignore`; no keys in code; check before each merge | Remove from history, rotate any exposed key | مصطفى |

---

## 3. Top Risks Summary

| Rank | Risk | Score | Next action |
|---|---|---|---|
| 1 | R01 Schedule pressure | 16 | Submit planning documents by 28 Oct and ask the lecturer about the extension |
| 2 | R02 Scope creep | 16 | Fix the freeze date (27 Nov) and mark MLOps items as Should in every plan |
| 3 | R03 Dataset limits | 15 | Draft the ERD and the synthetic table design by 31 Oct |
| 4 | R04 Synthetic data credibility | 12 | Add the synthetic flag to the data dictionary template |
| 5 | R05 Team availability | 12 | Confirm the backup for every role at the next sync |

---

## 4. Review Log

| Date | Change | By |
|---|---|---|
| 26 Oct 2026 | First version created | بثينه |
