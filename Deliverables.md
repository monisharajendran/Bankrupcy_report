# Model Performance Summary (Random Forest):
AUC--0.93, 
Precision (Bankrupt)-- High but conservative,
Recall (Bankrupt)--Strong sensitivity to risky firms,
F1-score--Balanced performance,
Confusion Matrix--Shows effective minority detection.

Hyperparameters: 400 trees improved stability & feature sampling diversity.max_depth=20 avoided overfitting while capturing complex interactions.class_weight="balanced" ensured bankrupt firms were not ignored. Overall, the model balances interpretability, performance, and computational efficiency.

# Interpretation of the global SHAP summary plots,highlighting the top 5 most influential features
ROA(C) Before Interest and Depreciation--Most influential feature.Low ROA strongly pushes predictions toward bankruptcy.

Persistent EPS in the Last Four Seasons--Measures earnings stability.Declining or volatile EPS increases bankruptcy risk.

Debt Ratio (%)--High leverage is a major financial distress indicator.

Net Value Growth Rate--Negative growth contributes positively to bankruptcy probability.

Cash Flow to Total Assets--Low operating cash flow increases risk despite profits.

This gives a more transparent understanding of model decision-making than Random Forest’s built-in importance.

# Explanations for the three selected local case studies, referencing the insights derived from the SHAP force plots for each.
Case 1 — High-risk company ---> Very low profitability (ROA, EPS all negative),Extremely high Debt Ratio,Poor cash flow generation
SHAP force plot: large red bars push prediction toward “Bankrupt”
Interpretation: Financial distress is driven by both structural leverage and severe earnings decline.

Case 2 — Low-risk company --->Strong ROA,Low leverage,Positive and stable cash flow
SHAP force plot: large blue bars counter bankruptcy risk
Interpretation: Healthy operations and stable financial structure strongly reduce risk.

Case 3 — Borderline company (Ambiguous case)--->Moderate ROA,Somewhat high debt,Mixed cash flow
SHAP force plot: both red and blue bars compete
Interpretation: This company sits in a gray zone — SHAP helps explain why the model does not confidently classify it.
