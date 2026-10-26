# Project Proposal: Customer Churn Intelligence & Retention System

| Item | Detail |
|---|---|
| Program | AI & Data Science, Data Scientist track ( DEPI) |
| Team | 6 members (see `task-assignment.md`) |
| Prepared by | Business Analyst (Bothina), with the project team |
| Version | 1.0 |
| Related documents | `project-plan.md`, `task-assignment.md`, `risk-register.md`, `kpis.md`, `docs/03-requirements/requirements.md` |

---

## 1. Overview

A subscription-based company is losing customers but does not know which customers are most likely to leave or which customer characteristics are associated with churn. This project delivers an end-to-end data science solution that analyzes churn patterns, estimates the churn risk of each customer, and supports retention decisions through an interactive dashboard and a prediction service.

## 2. Business Problem

Retaining an existing customer is generally argued to cost less than acquiring a new one, yet the company reacts only after customers have left. Management needs to answer four questions:

1. How serious is the churn problem, and where is it concentrated (segments, subscription types)?
2. Which customer characteristics are associated with churn?
3. Which current customers have the highest churn risk and should be contacted first?
4. What practical retention actions does the evidence support?

## 3. Objectives

1. Build a relational customer database (customers, subscriptions, billing, transactions, support tickets) and analyze it with SQL.
2. Clean the data and perform exploratory data analysis (EDA) to identify churn drivers.
3. Train and compare classification models (Logistic Regression, KNN, Decision Tree, SVM), and select the best one using a documented rule.
4. Assign each customer a churn probability and a risk tier (Low, Medium, High).
5. Deliver an interactive Plotly/Dash dashboard for business stakeholders.
6. Explain the findings and give evidence-based retention recommendations in a business report.
7. Track experiments and register the selected model with MLflow, expose predictions through FastAPI, and package the service with Docker and GitHub Actions (target extensions, built after the core deliverables).

## 4. Scope

### 4.1 In scope

| Area | Content |
|---|---|
| Data | Relational database, SQL scripts, data dictionary |
| Analysis | Cleaning, EDA, relationships between customer characteristics and churn |
| Machine learning | At least four classification models, imbalance handling, model comparison, selection rationale, risk tiers |
| Dashboard | Churn rate, churn by segment, churn by subscription type, churn trend, high-risk customer list |
| Reporting | Business problem definition, business report, README, technical documentation, user manual |
| Quality | Test plan, test cases, automated tests, bug reports |
| Extensions (Should) | MLflow tracking and registry, FastAPI `POST /predict`, Docker, GitHub Actions, cloud deployment |

### 4.2 Out of scope

- Real-time data streaming
- Automated retraining in production
- Mobile application

## 5. Stakeholders

| Stakeholder | Main need |
|---|---|
| Retention / Marketing Manager | Know who is likely to leave and where to spend the retention budget |
| Customer Success team | A prioritized list of high-risk customers |
| Executive / Business Owner | A one-screen view of churn, trends and revenue exposure |
| Course lecturer / evaluators | Complete documentation, working implementation, testing evidence |

The full analysis is in the Requirements document.

## 6. Data

The base dataset is the **IBM Telco Customer Churn** dataset (public). It provides one flat customer table with demographics, services, contract, billing and a churn label, and it has no calendar dates. The team will:

- Split it into linked relational tables (customers, subscriptions, billing).
- Generate **synthetic** transaction and support tables, because the project brief asks for SQL analysis of those sources. These tables are clearly marked in the data dictionary and are not treated as real customer evidence.
- Show churn trends by tenure group, since calendar dates are not available.

## 7. Approach

The project follows the data science lifecycle (CRISP-DM) taught in the program.

| Phase | Program course | Output |
|---|---|---|
| Business understanding | Data Science Methodology | Problem definition, KPIs, requirements |
| Data collection and storage | Databases and SQL for Data Science with Python | Database, SQL scripts |
| Data preparation and EDA | Python for Data Science, Data Analysis with Python | Clean dataset, EDA notebook |
| Visualization | Data Visualization with Python | Dashboard |
| Modeling and evaluation | Machine Learning with Python | Model comparison, selected model |
| Deployment and tracking | MLOps Tools, MLflow and Hugging Face | MLflow, API, Docker, CI/CD |
| Communication | Capstone Project | Business report, presentation |

## 8. Expected Deliverables

Business problem definition, SQL scripts, dataset and data dictionary, Jupyter analysis notebook, ML pipeline, model comparison, interactive dashboard, final business report, README, and (as extensions) MLflow experiments, FastAPI service, Dockerfile and GitHub Actions workflow. The documentation set follows the DEPI Project Documentation Guidelines.

## 9. Success Criteria

| Criterion | Measure |
|---|---|
| Model quality | Recall on the churn class meets the agreed target (provisional goal: at least 0.70), with Precision, F1, PR-AUC and ROC-AUC reported |
| Dashboard | All required views work and KPIs match independently calculated values |
| Documentation | All items required by the Guidelines delivered on time and uploaded to GitHub |
| Reproducibility | A reviewer can run the project from the README only |
| Business value | At least three evidence-based, reviewable retention recommendations |

Detailed KPIs and targets are in `kpis.md`.

## 10. Assumptions and Constraints

- The project must be delivered by 4 Dec 2026 by a team of 6.
- Only free and open-source tools are used.
- Core deliverables take priority over the optional extensions.
- Predictions support human decisions. They are model estimates, not guarantees, and are not used for automatic penalties against customers.

## 11. Timeline Summary

| Milestone | Date |
|---|---|
| M1: Planning, Literature Review, Requirements | 16 Oct 2026  |
| M2: System Analysis and Design | 6 Nov 2026 |
| M3: Implementation | 30 Nov 2026 |
| M4: Final presentation, testing and reports | 4 Dec 2026 |

The detailed Gantt chart is in `project-plan.md`.
