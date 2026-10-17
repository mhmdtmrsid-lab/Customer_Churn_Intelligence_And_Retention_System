# Requirements Gathering: Customer Churn Intelligence & Retention System

| Item | Detail |
|---|---|
| Document owner | Business Analyst (بثينه), with input from the ML Engineer and Data Analyst |
| Related documents | `docs/01-planning/proposal.md`, `docs/01-planning/project-plan.md`, `docs/02-literature/literature-review.md` |
| Scope reference | See Section 3 of the Project Proposal (in scope / out of scope) |

---

## 1. Stakeholder Analysis

### 1.1 Stakeholder Register

| ID | Stakeholder | Role in relation to the system | Main needs | Influence | Interest |
|---|---|---|---|---|---|
| S1 | Retention / Marketing Manager | Primary business user. Decides which customers to target and with what offer. | Know who is likely to leave, which segments are most affected, and where to spend the retention budget. | High | High |
| S2 | Customer Success / Support Team | Contacts at-risk customers and resolves service problems. | A clear, prioritized list of high-risk customers with the factors behind each prediction. | Medium | High |
| S3 | Executive / Business Owner | Monitors business performance and approves budget. | A one-screen view of churn rate, trends, and revenue exposure, plus clear recommendations. | High | Medium |
| S4 | Finance Team | Measures the cost of churn and the cost of retention campaigns. | Reliable churn figures and the ability to estimate campaign cost versus value. | Medium | Medium |
| S5 | Data / ML Team (project team) | Builds, maintains and improves the models and pipeline. | Reproducible pipeline, tracked experiments, versioned models, clean data. | High | High |
| S6 | IT / DevOps | Deploys and operates the service. | Containerized, documented, testable service with simple deployment steps. | Medium | Medium |
| S7 | Course Lecturer / Evaluators | Assess the project against the program criteria. | Complete documentation, working implementation, testing evidence, clear presentation. | High | High |
| S8 | Customers (indirect) | Receive retention actions. | Relevant offers, no intrusive or unfair treatment based on predictions. | Low | Medium |

### 1.2 Stakeholder Priority

| Quadrant | Stakeholders | Engagement approach |
|---|---|---|
| High influence, high interest (manage closely) | S1, S5, S7 | Involve in requirements, review each deliverable |
| High influence, medium interest (keep satisfied) | S3 | Provide executive summary and dashboard overview |
| Medium influence, high interest (keep informed) | S2 | Provide a usable high-risk list and clear explanations |
| Medium influence, medium interest (monitor) | S4, S6 | Share KPIs and deployment documentation |
| Low influence (consider) | S8 | Reflect in responsible-use requirements |

### 1.3 Assumption

The stakeholders above are hypothetical, since the project uses a public dataset. They represent the roles a real subscription-based company would have, as defined in the Project Proposal.

---

## 2. User Stories

Format: **As a** *role*, **I want** *capability*, **so that** *benefit*.
Priority uses MoSCoW: **M** Must, **S** Should, **C** Could.

### 2.1 Business Users

| ID | User story | Acceptance criteria | Priority |
|---|---|---|---|
| US-01 | As a Retention Manager, I want to see the overall churn rate, so that I can understand how serious the problem is. | The dashboard shows the churn rate as a percentage for the full customer base. | M |
| US-02 | As a Retention Manager, I want to see churn by customer segment, so that I can focus on the groups with the highest loss. | A chart shows churn rate by at least two segment attributes (for example tenure group, contract type). | M |
| US-03 | As a Retention Manager, I want to see churn by subscription type, so that I can find which plans lose the most customers. | A chart compares churn rate across subscription or contract types. | M |
| US-04 | As a Retention Manager, I want to see churn trends over time or tenure, so that I can tell whether the situation is improving. | A trend chart is shown, using tenure groups when dates are not available in the data. | M |
| US-05 | As a Customer Success agent, I want a list of high-risk customers, so that I know whom to contact first. | The list shows customer ID, predicted churn probability and risk tier, sorted from highest to lowest risk. | M |
| US-06 | As a Customer Success agent, I want to filter and sort the high-risk list, so that I can work on a specific segment. | The list can be filtered by at least contract type and risk tier. | S |
| US-07 | As a Customer Success agent, I want to see the main factors behind a customer's predicted risk, so that I can choose a suitable action. | For a selected customer, the top contributing factors are shown with careful wording (for example "factors driving the model's prediction"). | C |
| US-08 | As a Marketing Manager, I want to export the high-risk list, so that I can use it in a campaign. | The list can be downloaded as a CSV file. | S |
| US-09 | As an Executive, I want a one-page summary of key numbers, so that I can make decisions quickly. | The top of the dashboard shows the key KPIs (churn rate, number of high-risk customers, revenue exposure) without scrolling. | M |
| US-10 | As a Retention Manager, I want practical recommendations based on the findings, so that I know what to do next. | The final business report contains at least three evidence-based retention recommendations. | M |

### 2.2 Technical Users

| ID | User story | Acceptance criteria | Priority |
|---|---|---|---|
| US-11 | As a Data Scientist, I want to query the customer database with SQL, so that I can explore churn patterns. | The database contains linked tables and the SQL scripts run without errors. | M |
| US-12 | As a Data Scientist, I want to train and compare several classification models, so that I can choose the best one. | At least four models are trained and compared in one results table using the same metrics. | M |
| US-13 | As a Data Scientist, I want every experiment tracked, so that results are reproducible. | Parameters, metrics and artifacts for each run are recorded in MLflow. | S |
| US-14 | As a Data Scientist, I want to register the selected model with a version, so that the deployed model is traceable. | The chosen model appears in the MLflow Model Registry with a version number. | S |
| US-15 | As an Application Developer, I want to send customer data to an API and receive a prediction, so that I can integrate churn scoring into other tools. | `POST /predict` returns a churn probability and a risk tier for valid input. | S |
| US-16 | As a DevOps engineer, I want the service packaged in a container, so that it runs the same way everywhere. | `docker build` and `docker run` start the API using the README instructions. | S |
| US-17 | As a Developer, I want automated tests to run on every push, so that errors are caught early. | A GitHub Actions workflow runs the tests and fails when a test fails. | S |

### 2.3 Evaluator

| ID | User story | Acceptance criteria | Priority |
|---|---|---|---|
| US-18 | As an Evaluator, I want to run the project from the README, so that I can verify it works. | The README lists installation steps, requirements, configuration and an execution guide. | M |

---

## 3. Use Cases

### 3.1 Actors

| Actor | Description |
|---|---|
| Business User | Retention or Marketing Manager, Customer Success agent, or Executive who views insights |
| Data Scientist | Prepares data, trains models and selects the final model |
| Application Developer | Calls the prediction API from another tool |
| DevOps / MLOps Engineer | Builds, tests and deploys the service |

### 3.2 Use Case List

| ID | Use case | Primary actor |
|---|---|---|
| UC-01 | View churn overview dashboard | Business User |
| UC-02 | Explore churn by segment and subscription type | Business User |
| UC-03 | View and export high-risk customer list | Business User |
| UC-04 | Get churn prediction for a single customer | Business User, Application Developer |
| UC-05 | Prepare and clean data | Data Scientist |
| UC-06 | Train, compare and select models | Data Scientist |
| UC-07 | Track experiments and register model | Data Scientist, MLOps Engineer |
| UC-08 | Build, test and deploy the service | MLOps Engineer |

> These IDs will be reused in the Use Case Diagram in the System Analysis & Design phase.

### 3.3 Use Case Descriptions

#### UC-01: View churn overview dashboard

| Field | Description |
|---|---|
| Actor | Business User |
| Goal | See the overall churn situation at a glance |
| Preconditions | Dashboard is running and the cleaned data is loaded |
| Main flow | 1. User opens the dashboard. 2. System displays the KPI cards (churn rate, high-risk count). 3. System displays the churn trend chart. |
| Alternative flow | If data fails to load, the system shows an error message and no partial or misleading values. |
| Postcondition | User understands the current churn level |
| Related stories | US-01, US-04, US-09 |

#### UC-02: Explore churn by segment and subscription type

| Field | Description |
|---|---|
| Actor | Business User |
| Goal | Find which customer groups and plans lose the most customers |
| Preconditions | Dashboard is running |
| Main flow | 1. User selects a segment attribute or subscription type. 2. System updates the charts to show churn rate for the selection. 3. User compares groups. |
| Alternative flow | If a selected group has no customers, the system shows "no data for this selection". |
| Postcondition | User has identified high-churn groups |
| Related stories | US-02, US-03 |

#### UC-03: View and export high-risk customer list

| Field | Description |
|---|---|
| Actor | Business User |
| Goal | Identify and act on customers most likely to leave |
| Preconditions | A trained model has scored the customers |
| Main flow | 1. User opens the high-risk list. 2. System shows customers sorted by predicted probability with risk tier. 3. User applies filters. 4. User exports the list as CSV. |
| Alternative flow | If no customer exceeds the high-risk threshold, the system shows an empty-state message. |
| Postcondition | User has a prioritized list for retention action |
| Related stories | US-05, US-06, US-08 |

#### UC-04: Get churn prediction for a single customer

| Field | Description |
|---|---|
| Actor | Business User or Application Developer |
| Goal | Obtain the churn risk of one customer |
| Preconditions | The API is running and the registered model is loaded |
| Main flow | 1. Actor sends customer attributes to `POST /predict`. 2. System validates the input. 3. System applies the same preprocessing used in training. 4. System returns churn probability and risk tier. |
| Alternative flow | If input is missing or invalid, the system returns a clear error message and does not return a prediction. |
| Postcondition | Actor receives a prediction for the customer |
| Related stories | US-07, US-15 |

#### UC-05: Prepare and clean data

| Field | Description |
|---|---|
| Actor | Data Scientist |
| Goal | Produce a clean dataset ready for modeling |
| Preconditions | The database is built and accessible |
| Main flow | 1. Actor queries the data with SQL. 2. Actor handles missing and inconsistent values. 3. Actor encodes categorical variables and creates features. 4. Actor saves the cleaned dataset. |
| Alternative flow | If a column cannot be repaired, it is documented and dropped with a justification. |
| Postcondition | Cleaned dataset and data dictionary are available |
| Related stories | US-11 |

#### UC-06: Train, compare and select models

| Field | Description |
|---|---|
| Actor | Data Scientist |
| Goal | Select the best model using business-relevant metrics |
| Preconditions | Cleaned dataset exists |
| Main flow | 1. Actor splits the data. 2. Actor handles class imbalance. 3. Actor trains the models. 4. Actor evaluates them using Recall, F1, PR-AUC and ROC-AUC. 5. Actor compares results and selects a model with a written rationale. |
| Alternative flow | If no model reaches the target recall, the actor tunes the threshold or revisits features. |
| Postcondition | A selected model and a comparison table exist |
| Related stories | US-12 |

#### UC-07: Track experiments and register model

| Field | Description |
|---|---|
| Actor | Data Scientist, MLOps Engineer |
| Goal | Make experiments reproducible and the model versioned |
| Preconditions | Models are trained |
| Main flow | 1. Training code logs parameters, metrics and artifacts to MLflow. 2. Actor reviews runs in the MLflow interface. 3. Actor registers the selected model and assigns a version. |
| Alternative flow | If logging fails, the training run still completes and the error is reported. |
| Postcondition | The selected model is registered with a version |
| Related stories | US-13, US-14 |

#### UC-08: Build, test and deploy the service

| Field | Description |
|---|---|
| Actor | MLOps Engineer |
| Goal | Deliver a tested, containerized prediction service |
| Preconditions | A registered model and API code exist |
| Main flow | 1. Actor pushes code to GitHub. 2. GitHub Actions runs the automated tests. 3. The workflow builds the Docker image. 4. Actor runs or deploys the container. |
| Alternative flow | If a test fails, the workflow stops and reports the failure. |
| Postcondition | A working containerized service is available |
| Related stories | US-16, US-17 |

---

## 4. Functional Requirements

Priority uses MoSCoW: **M** Must, **S** Should, **C** Could.

### 4.1 Data Management

| ID | Requirement | Priority | Owner |
|---|---|---|---|
| FR-01 | The system shall store customer data in a relational database with separate linked tables for customers, subscriptions and billing, plus support and transaction tables where generated. | M | Data Engineer |
| FR-02 | The system shall provide SQL scripts that create the schema and load the data. | M | Data Engineer |
| FR-03 | The system shall provide SQL queries that analyze churn by customer, subscription and billing attributes. | M | Data Engineer |
| FR-04 | The system shall include a data dictionary describing every field, and shall clearly mark any synthetic tables or fields. | M | Data Engineer |

### 4.2 Data Preparation and Analysis

| ID | Requirement | Priority | Owner |
|---|---|---|---|
| FR-05 | The system shall detect and handle missing and inconsistent values and document each decision. | M | Data Analyst |
| FR-06 | The system shall encode categorical variables and scale numeric variables where required by the model. | M | Data Analyst |
| FR-07 | The system shall perform exploratory analysis including distributions, correlations and churn comparisons across groups. | M | Data Analyst |
| FR-08 | The system shall create additional features (for example tenure groups and service counts) and document them. | S | Data Analyst |

### 4.3 Machine Learning

| ID | Requirement | Priority | Owner |
|---|---|---|---|
| FR-09 | The system shall train at least four classification models: Logistic Regression, KNN, Decision Tree and SVM. | M | ML Engineer |
| FR-10 | The system shall handle class imbalance (class weights and threshold tuning, with SMOTE tested as an alternative). | M | ML Engineer |
| FR-11 | The system shall evaluate models using Precision, Recall, F1-score, ROC-AUC and PR-AUC, and shall present them in a comparison table. | M | ML Engineer |
| FR-12 | The system shall use a held-out test set that is not used for training or tuning. | M | ML Engineer |
| FR-13 | The system shall document the selected model and the rationale for selecting it. | M | ML Engineer |
| FR-14 | The system should additionally compare Random Forest and a gradient boosting model (XGBoost or LightGBM). | S | ML Engineer |
| FR-15 | The system shall assign each customer a churn probability and a risk tier (for example Low, Medium, High) based on defined thresholds. | M | ML Engineer |
| FR-16 | The system could provide per-customer explanations using SHAP, with wording that avoids causal claims. | C | ML Engineer |

### 4.4 Dashboard

| ID | Requirement | Priority | Owner |
|---|---|---|---|
| FR-17 | The dashboard shall display the overall churn rate. | M | Dashboard Developer |
| FR-18 | The dashboard shall display churn by customer segment. | M | Dashboard Developer |
| FR-19 | The dashboard shall display churn by subscription type. | M | Dashboard Developer |
| FR-20 | The dashboard shall display a churn trend chart. | M | Dashboard Developer |
| FR-21 | The dashboard shall display a high-risk customer list with probability and risk tier. | M | Dashboard Developer |
| FR-22 | The dashboard should allow filtering and sorting of the high-risk list. | S | Dashboard Developer |
| FR-23 | The dashboard should allow exporting the high-risk list as CSV. | S | Dashboard Developer |
| FR-24 | The dashboard shall present the main KPIs at the top of the page. | M | Dashboard Developer |

### 4.5 MLOps and Serving

| ID | Requirement | Priority | Owner |
|---|---|---|---|
| FR-25 | The system shall log parameters, metrics and artifacts of each training run to MLflow. | S | MLOps Engineer |
| FR-26 | The system shall register the selected model in the MLflow Model Registry with a version. | S | MLOps Engineer |
| FR-27 | The system shall expose a `POST /predict` endpoint that accepts customer attributes and returns a churn probability and risk tier. | S | MLOps Engineer |
| FR-28 | The API shall validate input and return clear error messages for invalid requests. | S | MLOps Engineer |
| FR-29 | The API shall provide a health-check endpoint. | S | MLOps Engineer |
| FR-30 | The API shall provide interactive API documentation. | S | MLOps Engineer |
| FR-31 | The system shall be packaged with a Dockerfile. | S | MLOps Engineer |
| FR-32 | The repository shall include a GitHub Actions workflow that runs automated tests on each push. | S | MLOps Engineer |

### 4.6 Reporting and Documentation

| ID | Requirement | Priority | Owner |
|---|---|---|---|
| FR-33 | The project shall deliver a business report that explains findings and recommendations to a non-technical stakeholder. | M | Business Analyst |
| FR-34 | The repository shall include a README with installation, requirements, configuration and execution steps. | M | All |
| FR-35 | The project shall include a test plan, test cases, automated tests and bug reports. | M | MLOps Engineer |
| FR-36 | The project shall include a user manual and technical documentation. | M | Dashboard Developer, MLOps Engineer |

---

## 5. Non-functional Requirements

Targets marked *(provisional)* will be confirmed after the baseline results and measurements are available.

### 5.1 Performance

| ID | Requirement | Target |
|---|---|---|
| NFR-01 | Single-customer API response time | Under 1 second on a standard laptop *(provisional)* |
| NFR-02 | Dashboard initial load time | Under 5 seconds on the project dataset *(provisional)* |
| NFR-03 | Dashboard chart and filter update time | Under 3 seconds *(provisional)* |
| NFR-04 | Model training time for the full model comparison | Completes on a standard laptop without specialized hardware |

### 5.2 Model Quality

| ID | Requirement | Target |
|---|---|---|
| NFR-05 | Recall on the churn class (the most important metric, since missing a churner is costly) | Target to be set after the baseline; provisional goal of at least 0.70 |
| NFR-06 | Model comparison fairness | All models use the same split, preprocessing and metrics |
| NFR-07 | Reproducibility | Fixed random seeds, so that results can be repeated |

### 5.3 Security and Privacy

| ID | Requirement | Target |
|---|---|---|
| NFR-08 | Personal data | No real personal identifiers are stored; customer IDs are anonymous |
| NFR-09 | Secrets management | No passwords, tokens or keys are committed to the repository |
| NFR-10 | Input validation | All API inputs are validated for type and range before use |
| NFR-11 | Dependency management | Dependencies are pinned in a requirements file |

### 5.4 Usability

| ID | Requirement | Target |
|---|---|---|
| NFR-12 | Dashboard clarity | A first-time business user can find the churn rate and the high-risk list without instructions |
| NFR-13 | Terminology | Business-friendly labels and short explanations for each chart |
| NFR-14 | Accessibility | Sufficient color contrast and readable font sizes; color is not the only way to convey meaning |
| NFR-15 | Documentation | A user manual with screenshots for the main tasks |

### 5.5 Reliability and Robustness

| ID | Requirement | Target |
|---|---|---|
| NFR-16 | Error handling | Failures produce clear messages and do not crash the application |
| NFR-17 | Consistent preprocessing | The API applies exactly the same preprocessing used during training |
| NFR-18 | Test coverage | Automated tests cover the data pipeline, the prediction function and the API endpoint |

### 5.6 Maintainability and Portability

| ID | Requirement | Target |
|---|---|---|
| NFR-19 | Code quality | Modular, commented code that follows consistent naming conventions |
| NFR-20 | Version control | Feature branches, pull requests and meaningful commit messages |
| NFR-21 | Portability | The service runs the same way on any machine through Docker |
| NFR-22 | Setup effort | A new developer can run the project by following the README only |

### 5.7 Responsible Use

| ID | Requirement | Target |
|---|---|---|
| NFR-23 | Wording of explanations | Explanations describe model behavior ("factors driving the prediction") and avoid claiming real-world causes |
| NFR-24 | Limitations | Limitations are documented in the final report, including the use of a public dataset and any synthetic tables |
| NFR-25 | Use of predictions | Predictions support human decisions and are not used for automatic penalties against customers |

---

## 6. Constraints and Assumptions

**Constraints**

- The project is limited to the program schedule (final delivery on 4 Dec 2026) and a team of 6 members.
- Only free and open-source tools are used.
- The project must use technologies covered by the program (Python, SQL, scikit-learn, Plotly/Dash, MLflow, FastAPI, Docker, GitHub Actions).

**Assumptions**

- The IBM Telco Customer Churn dataset is the base dataset. It has no calendar dates, so trends are shown by tenure groups.
- Support and transaction tables, if used, are generated synthetically and documented as such.
- Deployment to a cloud host (for example Hugging Face Spaces) is a target, and local Docker execution is the minimum.

**Out of scope** (as defined in the Project Proposal)

- Real-time data streaming
- Automated retraining in production
- Mobile application

---

## 7. Traceability to Project Objectives

| Project objective (from the Proposal) | Related requirements |
|---|---|
| 1. Relational database and SQL analysis | FR-01 to FR-04 |
| 2. Cleaning and EDA | FR-05 to FR-08 |
| 3. Train and compare models | FR-09 to FR-15, NFR-05 to NFR-07 |
| 4. Experiment tracking and model registry | FR-25, FR-26 |
| 5. Prediction API with Docker | FR-27 to FR-32 |
| 6. Interactive dashboard | FR-17 to FR-24 |
| 7. Retention recommendations | FR-33, US-10 |
