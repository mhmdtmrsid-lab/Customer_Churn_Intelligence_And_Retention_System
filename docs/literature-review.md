# Literature Review

## Customer Churn Intelligence & Retention System

*Machine learning for churn prediction, explainability, and retention decision-making*

---

## Summary

This review examines how the literature approaches customer churn prediction and what it implies for a system that predicts churn, explains it, and supports retention decisions. It covers problem definition, methodological evolution, commonly used models, predictive variables, class imbalance, evaluation metrics, explainable AI (XAI), and the step from prediction to action. It closes with research gaps and design implications for the proposed system.

Three conclusions stand out. First, tree-based ensemble models (XGBoost, LightGBM, CatBoost, Random Forest) are the dominant choice for structured churn data. Second, evaluation should be business-aligned rather than based on accuracy alone. Third, predicting who will leave is not the same as knowing whom to intervene on, which makes uplift modeling and cost-aware decision-making the most valuable direction for real deployment.

---

## 1. Problem Definition and Importance

Customer churn is the termination of a customer's relationship with a company within a defined period, for example by cancelling a subscription, ceasing to purchase, or moving to a competitor. The literature distinguishes two settings (Buckinx & Van den Poel, 2005):

- **Contractual churn:** the customer formally ends a relationship, as with a telecom or SaaS subscription. The churn event is observable and dated.
- **Non-contractual churn:** the customer simply stops buying, as with an online store. Churn must be inferred from inactivity, which makes the definition of "churned" a modeling decision in itself.

Churn affects revenue and Customer Lifetime Value, and it is commonly argued that retaining an existing customer costs less than acquiring a new one (Reichheld & Sasser, 1990). This claim is widely repeated, but the specific multipliers that circulate in practice are not consistently supported, so it should be treated as a general argument rather than a fixed ratio. The practical consequence is a shift from reacting after a customer leaves to predicting departure early and intervening, for example through a retention offer, a customer-service call, or a service fix.

---

## 2. Evolution of Prediction Methods

Research on churn prediction can be summarized in four overlapping phases. The table below is a simplification; real studies often combine approaches.

| Phase | Typical methods | Strengths | Limitations |
|---|---|---|---|
| Traditional statistical | Logistic Regression, Decision Trees, rule-based systems | Simple, interpretable, good baselines | Limited ability to capture non-linear relationships and interactions |
| Classical machine learning | SVM, Random Forest, boosting (XGBoost, LightGBM, CatBoost) | Strong performance on tabular data, handles interactions | Needs careful preprocessing and imbalance handling |
| Deep learning | ANN, CNN, RNN/LSTM, Transformers | Suited to sequential, textual and interaction-log data | Harder to interpret, needs more data and compute |
| Decision-oriented | XAI (SHAP, LIME), profit-driven metrics, uplift modeling, adaptive learning | Links predictions to explanations and business value | Limited adoption in deployed systems |

Early benchmark work showed that ensemble methods such as bagging and boosting improved churn prediction over single classifiers (Lemmens & Croux, 2006), and comparative studies of machine learning techniques followed (Vafeiadis et al., 2015). Industry-wide model comparisons such as the Teradata churn tournament underlined that predictive accuracy depends on the method, the data, and the evaluation design (Neslin et al., 2006).

---

## 3. Most Commonly Used Models

A systematic review of recent studies (2020–2024) screened 240 studies for bibliometric analysis and 61 for detailed synthesis, following PRISMA 2020. It found that ensemble methods such as XGBoost and LightGBM remain dominant among machine learning approaches, while deep learning models such as LSTM and CNN are increasingly applied to complex data (Imani et al., 2025).

- **Gradient boosting:** XGBoost (Chen & Guestrin, 2016), LightGBM (Ke et al., 2017) and CatBoost (Prokhorenkova et al., 2018) are the most frequently used for structured data, offering a good balance of accuracy, speed and ease of deployment.
- **Random Forest and Logistic Regression:** common as strong and interpretable baselines.
- **Deep learning:** LSTM for sequences of customer behavior, CNN for pattern extraction, and NLP for complaints, reviews and support messages.

Reported performance varies widely across studies. Because datasets, churn definitions, class ratios and validation designs differ, headline figures from separate papers are not directly comparable and should not be treated as a universal accuracy range.

---

## 4. Data and Predictive Variables

The quality of the data and the definition of churn matter more than the choice of algorithm. The variables that recur across the literature fall into these groups:

| Variable group | Examples |
|---|---|
| Demographic | Age, gender, location, customer type |
| Contract and financial | Plan type, contract length, payment method, monthly charges, billing history |
| Usage and behavior | Calls, data volume, session duration, purchase frequency, Recency–Frequency–Monetary (RFM) features, change in usage over time |
| Interaction and service | Complaints, support tickets, customer-service calls, ratings, app engagement |
| Social and network | Influence of connected customers, especially in telecom (Verbeke et al., 2014) |
| Text and sentiment | Reviews, comments, support messages |

Contractual, financial and behavioral variables are among the most consistently informative. Engineered temporal features, such as the change in usage over the last 30 to 60 days, often add predictive value beyond static attributes. Models should also be validated on a later time period than the one used for training, since random splits can leak future information and overstate performance.

---

## 5. Class Imbalance

Churners are usually a minority of the customer base, for example 20% churners against 80% retained. Accuracy then becomes misleading: a model that predicts that everyone will stay can score high accuracy while identifying no churners at all (Burez & Van den Poel, 2009). Common remedies include:

- Oversampling, such as SMOTE (Chawla et al., 2002) and ADASYN.
- Undersampling of the majority class.
- Class weights applied during training.
- Decision-threshold tuning.
- Cost-sensitive learning, where missing a churner is penalized more than a false alarm.

Evidence on resampling is mixed. Studies report gains when rebalancing is combined with Random Forest or boosting, but resampling can overfit and can distort the calibration of predicted probabilities, which matters when probabilities feed a cost calculation. Class weights combined with threshold tuning are often a simpler and competitive alternative, and any chosen approach should be validated on untouched, realistically distributed test data.

---

## 6. Evaluation Metrics

Accuracy alone is not adequate for churn. The literature recommends a set of complementary, business-relevant measures.

| Metric | What it tells us | Why it matters |
|---|---|---|
| Precision | Of customers flagged as churners, how many truly leave | Controls wasted retention spend |
| Recall | Of customers who truly leave, how many are caught | Controls missed churners |
| F1-score | Balance of precision and recall | Single summary under imbalance |
| ROC-AUC | Overall ability to rank churners above non-churners | Threshold-independent comparison |
| PR-AUC | Precision–recall trade-off across thresholds | More informative than ROC-AUC when positives are rare (Saito & Rehmsmeier, 2015) |
| Lift / top-decile lift | Churn concentration among the highest-scored customers | Reflects targeted campaign performance (Neslin et al., 2006) |
| Expected Maximum Profit (EMP) | Expected profit from a retention campaign given costs and benefits | Aligns model choice with financial outcome (Verbeke et al., 2012; Verbraken et al., 2013) |

The central point is that the best model is not simply the most accurate one. It is the one that lets a company direct a limited retention budget toward the customers where intervention creates value.

---

## 7. Explainability (XAI)

Marketing and customer-service teams need to know why a customer is at risk, not only that they are. Model-agnostic methods such as SHAP (Lundberg & Lee, 2017) and LIME (Ribeiro et al., 2016) are the most widely used. SHAP provides consistent global and local attributions; LIME fits a simple local surrogate around a single prediction. A typical output reads: *"This customer has a 78% predicted churn probability, driven mainly by high monthly charges and declining usage over the last 60 days."*

### An important caution

SHAP and LIME explain how a model reaches its predictions, not how the real world works. A review of business-research papers that used these tools flagged statements such as "feature X increases customer churn" as misuse, because they turn a model-level explanation into a claim about real-world relationships (Ragodos et al., 2024). For a dashboard, this means wording such as "factors driving the model's prediction" rather than "reasons the customer left," and avoiding causal language unless supported by experimental evidence.

The recent systematic review also reports that explainable AI and adaptive learning show promise but remain little adopted in real-world deployments (Imani et al., 2025).

---

## 8. From Prediction to Retention

Prediction alone does not solve churn. Value comes from connecting the model to a decision and intervention process. A practical system can be organized in four layers:

1. **Data layer:** collect, clean and unify customer data, and build temporal features.
2. **Modeling layer:** train several models, handle imbalance, and select using recall, PR-AUC and business impact.
3. **Explanation layer:** use SHAP or LIME to show the factors behind each prediction, with careful wording.
4. **Action and dashboard layer:** group customers into risk tiers, recommend an action per segment, and measure campaign results.

### Risk is not the same as treatability

A key finding is that targeting the customers at highest risk of churning can be ineffective, because some high-risk customers will leave regardless of intervention and some may even react negatively to being contacted (Ascarza, 2018). What matters is the incremental effect of the intervention. This motivates uplift (incremental response) modeling, which estimates who is persuadable, and it changes the dashboard question from "who will leave?" to "who is worth spending on?"

---

## 9. Research Gaps

| Gap | Description |
|---|---|
| Real-world deployment | Many studies evaluate models on static or public datasets; few report operational deployment and measured business results. |
| Intervention effectiveness | Predicting churn risk is common; estimating the causal effect of retention actions (uplift) is rare (Ascarza, 2018). |
| Concept drift | Customer behavior changes over time, so models need monitoring and periodic retraining or adaptive learning (Gama et al., 2014). |
| Interpretation validity | Post hoc explanations are often over-interpreted as real-world causes (Ragodos et al., 2024). |
| Business-aligned evaluation | Heavy reliance on accuracy and AUC instead of profit and intervention cost (Verbraken et al., 2013). |
| Temporal validation | Random train–test splits can leak future information; time-based validation is less common. |
| Real-time data | Few systems monitor behavior continuously and trigger timely interventions. |
| Generalizability | A model tuned for telecom may not transfer to banking or e-commerce without redesign. |

---

## 10. Implications for the Proposed System

The project is well supported by the literature: it turns customer data into an explainable prediction and then into a practical retention action. The literature suggests building it in stages.

| Stage | Scope |
|---|---|
| Stage 1: baseline | Logistic Regression and Random Forest as baselines, compared with XGBoost or LightGBM. Handle imbalance with class weights and threshold tuning, testing SMOTE as an alternative. Evaluate with Recall, F1, PR-AUC and ROC-AUC, using a time-based split where dates are available. |
| Stage 2: explanation | Add SHAP for global and per-customer explanations in an interactive dashboard, with cautious wording that avoids causal claims. |
| Stage 3: decision value | Add profit-based evaluation (EMP-style cost–benefit logic), risk tiers with recommended actions, and uplift modeling to prioritize customers who are likely to respond to intervention. |
| Stage 4: operations | Monitor drift, retrain periodically, and track campaign outcomes to close the loop. |

Taken together, the system would answer four questions: who is likely to leave, which factors drive that prediction, how severe the risk is, and which action is most worthwhile. Positioned this way, it addresses two documented gaps: the link between prediction and decision, and responsible explanation.

---

## References

- Ascarza, E. (2018). Retention futility: Targeting high-risk customers might be ineffective. *Journal of Marketing Research, 55*(1), 80–98.
- Buckinx, W., & Van den Poel, D. (2005). Customer base analysis: Partial defection of behaviourally loyal clients in a non-contractual FMCG retail setting. *European Journal of Operational Research, 164*(1), 252–268.
- Burez, J., & Van den Poel, D. (2009). Handling class imbalance in customer churn prediction. *Expert Systems with Applications, 36*(3), 4626–4636.
- Chawla, N. V., Bowyer, K. W., Hall, L. O., & Kegelmeyer, W. P. (2002). SMOTE: Synthetic minority over-sampling technique. *Journal of Artificial Intelligence Research, 16*, 321–357.
- Chen, T., & Guestrin, C. (2016). XGBoost: A scalable tree boosting system. *Proceedings of the 22nd ACM SIGKDD International Conference on Knowledge Discovery and Data Mining*, 785–794.
- Gama, J., Žliobaitė, I., Bifet, A., Pechenizkiy, M., & Bouchachia, A. (2014). A survey on concept drift adaptation. *ACM Computing Surveys, 46*(4), Article 44.
- Imani, M., Joudaki, M., Beikmohammadi, A., & Arabnia, H. R. (2025). Customer churn prediction: A systematic review of recent advances, trends, and challenges in machine learning and deep learning. *Machine Learning and Knowledge Extraction, 7*(3), 105. https://doi.org/10.3390/make7030105
- Ke, G., Meng, Q., Finley, T., Wang, T., Chen, W., Ma, W., Ye, Q., & Liu, T.-Y. (2017). LightGBM: A highly efficient gradient boosting decision tree. *Advances in Neural Information Processing Systems, 30*.
- Lemmens, A., & Croux, C. (2006). Bagging and boosting classification trees to predict churn. *Journal of Marketing Research, 43*(2), 276–286.
- Lundberg, S. M., & Lee, S.-I. (2017). A unified approach to interpreting model predictions. *Advances in Neural Information Processing Systems, 30*, 4765–4774.
- Neslin, S. A., Gupta, S., Kamakura, W., Lu, J., & Mason, C. H. (2006). Defection detection: Measuring and understanding the predictive accuracy of customer churn models. *Journal of Marketing Research, 43*(2), 204–211.
- Prokhorenkova, L., Gusev, G., Vorobev, A., Dorogush, A. V., & Gulin, A. (2018). CatBoost: Unbiased boosting with categorical features. *Advances in Neural Information Processing Systems, 31*.
- Ragodos, R., et al. (2024). From model explanation to data misinterpretation: A cautionary analysis of post hoc explainers in business research. *arXiv:2408.16987*. https://arxiv.org/abs/2408.16987
- Reichheld, F. F., & Sasser, W. E. (1990). Zero defections: Quality comes to services. *Harvard Business Review, 68*(5), 105–111.
- Ribeiro, M. T., Singh, S., & Guestrin, C. (2016). "Why should I trust you?" Explaining the predictions of any classifier. *Proceedings of the 22nd ACM SIGKDD International Conference on Knowledge Discovery and Data Mining*, 1135–1144.
- Saito, T., & Rehmsmeier, M. (2015). The precision-recall plot is more informative than the ROC plot when evaluating binary classifiers on imbalanced datasets. *PLOS ONE, 10*(3), e0118432.
- Vafeiadis, T., Diamantaras, K. I., Sarigiannidis, G., & Chatzisavvas, K. C. (2015). A comparison of machine learning techniques for customer churn prediction. *Simulation Modelling Practice and Theory, 55*, 1–9.
- Verbeke, W., Dejaeger, K., Martens, D., Hur, J., & Baesens, B. (2012). New insights into churn prediction in the telecommunication sector: A profit driven data mining approach. *European Journal of Operational Research, 218*(1), 211–229.
- Verbeke, W., Martens, D., & Baesens, B. (2014). Social network analysis for customer churn prediction. *Applied Soft Computing, 14*, 431–446.
- Verbraken, T., Verbeke, W., & Baesens, B. (2013). A novel profit maximizing metric for measuring classification performance of customer churn prediction models. *IEEE Transactions on Knowledge and Data Engineering, 25*(5), 961–973.

<!-- Verification note: Imani et al. (2025) and Ragodos et al. (2024, arXiv) were confirmed through search. The remaining references are well-known works cited from memory; confirm volume, page numbers and DOIs against the original sources (e.g. Google Scholar) before submission. Delete this comment afterwards. -->
