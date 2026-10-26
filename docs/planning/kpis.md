# Key Performance Indicators (KPIs)

| Item | Detail |
|---|---|
| Project | Customer Churn Intelligence & Retention System |
| Document owner | Business Analyst (Bothina) |
| Version | 1.0 |
| Related documents | `proposal.md`, `risk-register.md`, `docs/03-requirements/requirements.md` |

Targets marked **(provisional)** are confirmed after the baseline results and measurements are available, as stated in the Requirements document.

---

## 1. Purpose

These KPIs define how the team decides whether the project succeeded. They cover the model, the system, quality, delivery, and documentation. A separate section (Section 7) lists the business KPIs that the dashboard itself reports to stakeholders.

---

## 2. Model Performance KPIs

| ID | KPI | Target | How it is measured | Owner | Frequency |
|---|---|---|---|---|---|
| K-M1 | Recall on the churn class | At least 0.70 (provisional) | Held-out test set, same split for all models | محمد | After each model run |
| K-M2 | Precision on the churn class | Minimum value set after the baseline (provisional) | Held-out test set | محمد | After each model run |
| K-M3 | F1-score | Used to choose between models with similar Recall (FR-38) | Held-out test set | محمد | After each model run |
| K-M4 | PR-AUC and ROC-AUC | Reported for every model; selected model is not worse than the baseline | Held-out test set | محمد | After each model run |
| K-M5 | Models compared | At least 4 (Logistic Regression, KNN, Decision Tree, SVM) | Count of models in the comparison table | محمد | Once, at M3 |
| K-M6 | Evaluation integrity | 100% of preprocessing steps fitted on training data only | Notebook review by a second member | مريم | Before M3 |

---

## 3. System Performance KPIs

| ID | KPI | Target | How it is measured | Owner | Frequency |
|---|---|---|---|---|---|
| K-S1 | API response time for one customer | Under 1 second (provisional, NFR-01) | Timing of `POST /predict` on a standard laptop | مصطفى | Before M3 |
| K-S2 | Dashboard initial load time | Under 5 seconds (provisional, NFR-02) | Manual timing on the project dataset | بسمله | Before M3 |
| K-S3 | Dashboard filter and chart update time | Under 3 seconds (provisional, NFR-03) | Manual timing | بسمله | Before M3 |
| K-S4 | Demo availability during evaluation | The deployed demo or local Docker run works at the time of presentation | Test run one day before and on the day | مصطفى | Before M4 |

---

## 4. Quality and Testing KPIs

| ID | KPI | Target | How it is measured | Owner | Frequency |
|---|---|---|---|---|---|
| K-Q1 | Must requirements covered by test cases | 100% | Traceability between requirement IDs and test cases (FR-45) | مصطفى | Before M3 and M4 |
| K-Q2 | Automated tests passing | 100% on `main` | GitHub Actions result (or local test run if CI is not completed) | مصطفى | Every push |
| K-Q3 | Dashboard KPIs match independent calculation | 100% of KPI values match SQL or pandas results | Test cases comparing both | بسمله, مريم | Before M3 |
| K-Q4 | Open critical bugs at delivery | 0 | Bug report log | مصطفى | Before M4 |
| K-Q5 | Test coverage of the prediction function, data pipeline and API | Each covered by at least one automated test (NFR-18) | Test files review | مصطفى | Before M3 |

---

## 5. Delivery and Process KPIs

| ID | KPI | Target | How it is measured | Owner | Frequency |
|---|---|---|---|---|---|
| K-D1 | Milestones delivered on time | 4 of 4 (M1 to M4) | Milestone table in `project-plan.md` | Project lead | At each milestone |
| K-D2 | Deliverables with a named owner and reviewer | 100% | `task-assignment.md` | بثينه | Once, then at each sync |
| K-D3 | Pull requests reviewed before merge | 100% | GitHub pull request history | مصطفى | Weekly |
| K-D4 | Critical and high risks with an active mitigation | 100% | `risk-register.md` | بثينه | Weekly |
| K-D5 | Weekly sync held | At least 1 per week | Meeting notes | Project lead | Weekly |

---

## 6. Documentation and Usability KPIs

| ID | KPI | Target | How it is measured | Owner | Frequency |
|---|---|---|---|---|---|
| K-U1 | Documentation items from the Guidelines delivered | 100% of required items, on GitHub | Checklist against the Guidelines | بثينه | At each milestone |
| K-U2 | README run-through | A member who did not write it runs the project from the README only, without help | One test run, notes recorded | مصطفى | Before M3 |
| K-U3 | Dashboard usability check | At least 3 people outside the team find the churn rate and the high-risk list without instructions (NFR-12) | Short observed test | بسمله | Before M4 |
| K-U4 | Retention recommendations | At least 3, each with finding, segment, action and review measure (FR-40) | Business report review | بثينه | Before M4 |
| K-U5 | Limitations documented | Dataset limits, synthetic tables and the meaning of risk tiers stated in the report (NFR-24) | Business report review | بثينه | Before M4 |

---

## 7. Business KPIs Reported by the Dashboard

These are the measures the system shows to stakeholders (defined in FR-41). They are product outputs, not project-success targets.

| ID | KPI | Definition | Audience |
|---|---|---|---|
| B-1 | Churn rate | Churned customers divided by all customers | Retention Manager, Executive |
| B-2 | High-risk customers | Number of customers in the High risk tier | Customer Success, Retention Manager |
| B-3 | Revenue exposure | Sum of monthly charges of High-tier customers | Executive, Finance |
| B-4 | Churn by segment | Churn rate per segment (for example tenure group, contract type) | Retention Manager |
| B-5 | Churn by subscription type | Churn rate per subscription or contract type | Retention Manager |

---

## 8. Reporting and Review

- The owner of each KPI updates its status in the weekly sync.
- Status values: **Not started**, **On track**, **At risk**, **Met**, **Not met**.
- A KPI marked **At risk** is added to `risk-register.md` with a mitigation.
- Provisional targets are confirmed in the model evaluation report and then recorded here with the date.

### 8.1 Status Tracker

| ID | Status | Last updated |
|---|---|---|
| K-M1 to K-M6 | Not started | 26 Oct 2026 |
| K-S1 to K-S4 | Not started | 26 Oct 2026 |
| K-Q1 to K-Q5 | Not started | 26 Oct 2026 |
| K-D1 to K-D5 | On track | 26 Oct 2026 |
| K-U1 to K-U5 | On track | 26 Oct 2026 |
