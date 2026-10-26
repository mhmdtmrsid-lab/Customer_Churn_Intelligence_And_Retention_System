# Task Assignment & Roles

| Item | Detail |
|---|---|
| Project | Customer Churn Intelligence & Retention System |
| Document owner | Business Analyst (بثينه) |
| Version | 1.0 |
| Related documents | `project-plan.md`, `risk-register.md`, `docs/03-requirements/requirements.md` |

---

## 1. Team and Roles

| Member | Role | Main responsibilities | Backup |
|---|---|---|---|
| عبدالله | Data Engineer | Database design and creation, SQL scripts, synthetic transaction and support tables, data dictionary | مريم |
| مريم | Data Analyst | Data cleaning, EDA, feature engineering, churn driver analysis, literature review, data-flow documentation | عبدالله |
| محمد | ML Engineer | Model training and comparison, imbalance handling, evaluation, model selection, risk tiers | مريم |
| مصطفى | MLOps Engineer | MLflow, FastAPI, Docker, GitHub Actions, deployment, testing plan and automated tests | محمد |
| بسمله | Dashboard / Frontend | Plotly Dash dashboard, wireframes, UI/UX guidelines, user manual | مصطفى |
| بثينه | Business Analyst | Business problem and KPIs, stakeholders, requirements, risk register, retention recommendations, business report, presentation | بسمله |

**Project lead:** to be confirmed by the team. The lead tracks deadlines, runs the weekly sync and reports delays (see the Working Agreement in `project-plan.md`).

---

## 2. Responsibility Matrix by Deliverable

**O** = Owner (writes it), **R** = Reviewer (checks it before merge).

### 2.1 Project Planning & Management (due 16 Oct 2026, submitted by 28 Oct)

| Deliverable | Owner | Reviewer |
|---|---|---|
| Project Proposal | بثينه | محمد |
| Project Plan (Gantt, milestones, resources) | بثينه | مصطفى |
| Task Assignment & Roles | بثينه | All |
| Risk Assessment & Mitigation Plan | بثينه | مصطفى |
| KPIs | بثينه | محمد |

### 2.2 Literature Review (due 16 Oct 2026)

| Deliverable | Owner | Reviewer |
|---|---|---|
| Literature Review | مريم | بثينه |
| Feedback & Evaluation, Suggested Improvements, Final Grading Criteria | Lecturer (placeholder file kept by بثينه) | : |

### 2.3 Requirements Gathering (due 16 Oct 2026)

| Deliverable | Owner | Reviewer |
|---|---|---|
| Stakeholder Analysis | بثينه | محمد |
| User Stories & Use Cases | بثينه | بسمله |
| Functional Requirements | بثينه | محمد, مصطفى |
| Non-functional Requirements | بثينه | مصطفى |

### 2.4 System Analysis & Design (due 6 Nov 2026)

| Deliverable | Owner | Reviewer |
|---|---|---|
| Problem Statement & Objectives | بثينه | محمد |
| Functional & Non-Functional Requirements (design copy) | بثينه | مصطفى |
| Use Case Diagram & Descriptions | بثينه | بسمله |
| Software Architecture | مصطفى | محمد |
| ER Diagram | عبدالله | مريم |
| Logical & Physical Schema | عبدالله | مريم |
| DFD (context level and detailed levels) | مريم | عبدالله |
| Sequence Diagrams | مصطفى | بسمله |
| Activity Diagram: data preparation | مريم | عبدالله |
| Activity Diagram: model training | محمد | مريم |
| State Diagram (customer lifecycle: Active, At-risk, Churned) | مريم | بثينه |
| Class Diagram | محمد | مصطفى |
| Wireframes & Mockups | بسمله | بثينه |
| UI/UX Guidelines | بسمله | بثينه |
| Technology Stack | بثينه | مصطفى |
| Deployment Diagram | مصطفى | محمد |
| Component Diagram | مصطفى | محمد |
| API Documentation | مصطفى | بسمله |
| Testing & Validation plan (unit, integration, UAT) | مصطفى, بثينه (UAT) | محمد |
| Deployment Strategy | مصطفى | محمد |

### 2.5 Implementation (due 30 Nov 2026)

| Deliverable | Owner | Reviewer |
|---|---|---|
| Database and SQL scripts | عبدالله | مريم |
| Data dictionary | عبدالله | مريم |
| Cleaning and EDA notebook | مريم | محمد |
| ML pipeline and model comparison | محمد | مريم |
| Dashboard | بسمله | بثينه |
| MLflow tracking and model registry | مصطفى | محمد |
| FastAPI service | مصطفى | محمد |
| Dockerfile and GitHub Actions workflow | مصطفى | عبدالله |
| README (installation, requirements, configuration, execution guide, API docs, deployment link) | مصطفى | All (one member runs it from scratch) |
| Coding standards and branching strategy (`CONTRIBUTING.md`) | مصطفى | All |

### 2.6 Testing, Final Presentation and Reports (due 4 Dec 2026)

| Deliverable | Owner | Reviewer |
|---|---|---|
| Test Cases & Test Plan | مصطفى | بثينه |
| Automated tests | مصطفى | محمد |
| Bug reports | All (reporter), owner of the faulty part (fixer) | مصطفى |
| User Manual | بسمله | بثينه |
| Technical Documentation | مصطفى, محمد | عبدالله |
| Business Report | بثينه | مريم |
| Project Presentation | بثينه (lead), All (own sections) | All |
| Video Demonstration (optional) | بسمله | بثينه |

---

## 3. Collaboration Rules

1. **One owner per deliverable.** The owner is accountable for completing it by the due date; helpers are named in the plan.
2. **Pull requests.** Every file is added through a pull request on a feature branch. The reviewer in the tables above approves it before merging into `main`.
3. **Definition of done.** A deliverable is done when it is on `main`, follows the project template, is linked from the README, and has been reviewed.
4. **Weekly sync.** The team reviews progress against `project-plan.md`, updates `risk-register.md` and checks the KPIs in `kpis.md`.
5. **Delays.** An owner who expects to miss a due date by more than 2 days tells the project lead immediately, and the backup member takes over if needed.
6. **Consistency.** Requirement IDs (FR, NFR, US, UC) are used as they appear in the Requirements document when writing design, test and report documents.

---

## 4. Immediate Actions (26 to 28 Oct 2026)

| Action | Owner |
|---|---|
| Create repository structure and add collaborators | مصطفى |
| Upload proposal, plan, task assignment, risk register, KPIs | بثينه |
| Apply the three Literature Review edits and add the feedback placeholder file | مريم |
| Ask the lecturer for the Grading Criteria and the meaning of the Literature Review section | بثينه |
| Download the dataset and draft the ERD | عبدالله |
| Run a first baseline model on the Telco data | محمد |
| Create the Mermaid or draw.io diagram templates for the team | مصطفى |
