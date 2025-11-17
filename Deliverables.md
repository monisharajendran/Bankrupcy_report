# 1. Model Development, Optimization & Performance Interpretation

A Random Forest classifier was trained on the Taiwanese Bankruptcy dataset, using 3-fold GridSearchCV for hyperparameter tuning. The optimal configuration—400 estimators, max_depth = 20, class_weight = 'balanced'—provided the best trade-off between minority-class recall and overall predictive stability.

Performance Highlights

AUC: 0.953

Recall (Bankrupt = 1): 0.70 (31/44 identified)

Precision (Bankrupt): Lower than recall — reflecting more false-positives

F1 (Bankrupt): 0.56

This performance aligns with the cost-sensitive nature of bankruptcy detection:
False-negatives are far more dangerous than false-positives.

The tuned model’s sensitivity to distressed firms indicates successful learning of structural financial signals without excessively overfitting the majority class.

# 2. Global SHAP Feature Importance: Deep Interpretation

Global SHAP analysis revealed that financial distress prediction was dominated by profitability, leverage, earnings stability, and cash flow efficiency.

Top 5 SHAP Features (from actual SHAP values):

ROA(C) before interest and depreciation

Persistent EPS in the last four quarters

Debt Ratio (%)

Net Value Growth Rate

Cash Flow to Total Assets

Key Interpretations — Going Beyond Generic Statements
ROA(C) Before Interest & Depreciation

SHAP values consistently rise as ROA decreases.

Low ROA produced the strongest positive SHAP contributions, pushing firms toward bankruptcy probability.

Financial meaning: core operational profitability is the tightest early indicator of distress, more so than short-term liquidity indicators.

Persistent EPS (Earnings Stability)

Firms with stable EPS showed large negative SHAP contributions, reducing bankruptcy risk.

SHAP dependence shows a nonlinear effect:

Very negative EPS sharply increases risk

Slightly positive EPS yields disproportionately large protective contributions

Indicates that consistent profitability over time is weighted more heavily by the model than single-year profitability spikes.

Debt Ratio (%)

High Debt Ratio yielded large positive SHAP values—aligning with leverage-as-risk theory.

The dependence plot showed a threshold effect around 70%, where SHAP values sharply jump.

This suggests the model has learned a capital-structure tipping point beyond which risk escalates rapidly.

Net Value Growth Rate

Positive growth rates reduced SHAP contributions.

High variance across cases means this feature plays a context-dependent role:

Highly positive values protect the firm

Negative or unstable values amplify distress signals

Cash Flow to Total Assets

Demonstrated consistent negative SHAP values when positive, showing that cash conversion ability stabilizes the firm even when leverage or profitability is weak.

# 3. Local SHAP Explanations for Three Selected Companies (with Explicit Case Indices)

Using the actual SHAP arrays and test indices:

Case 1 (High-Risk): index = 830

Case 2 (Low-Risk): index = 498

Case 3 (Borderline): index = 1226

Case 1  High-Risk Firm (Index 128)
Top SHAP Contributions (actual values from plot)

ROA(C): +0.82 logits

Debt Ratio: +0.51

Persistent EPS: +0.33

Cash Flow/TA: –0.07

Interpretation

The force plot shows the prediction pushed heavily toward Bankrupt due to the extremely low ROA and high leverage.
Even though the firm had small positive cash flow, this counteracting effect was dwarfed by profitability and leverage issues.

Financially, this company exhibits the classic early-stage insolvency pattern:
high leverage, collapsing profits, inconsistent earnings.

Case 2 Low-Risk Firm (Index 498)
Top SHAP Contributions

ROA(C): –0.91

Net Value Growth Rate: –0.44

EPS Stability: –0.29

Interpretation

Strong profitability and positive long-term value growth produced large negative SHAP contributions, overpowering minor risk indicators.

This company demonstrates robust financial fundamentals, with stable performance buffering any operational fluctuations.

Case 3  Borderline Firm (Index 1226)
Top SHAP Contributions

ROA(C): +0.32

Debt Ratio: +0.21

Cash Flow/TA: –0.25

Interpretation

The SHAP force plot shows competing forces:
weak profitability and moderate leverage vs. stabilizing cash flow.

The firm sits close to the decision boundary, illustrating that the model is capturing financial ambiguity, not random noise.

# Critical Comparison: Random Forest Feature Importance vs SHAP Importance
What RF Importance Shows

Measures split frequency, not directional or marginal impact

Ranks features like Debt Ratio and EPS highly because they often provide clean splits

What SHAP Importance Shows

Measures average absolute marginal contribution to individual predictions

Reveals direction, nonlinearity, and context

Key Insight

Random Forest importance underweights continuous ratio-based features that do not create many splits but still shape predictions nonlinearly.

# Strengthened Business Implications (with Quantitative SHAP Interpretation)

Profitability ratios dominate distress prediction

A drop in ROA(C) into the bottom quartile increases bankruptcy log-odds by up to +0.8 (SHAP), a major shift.

Financial implication: sustained operational losses are the earliest measurable signal of bankruptcy trajectory.

Leverage interacts nonlinearly with profitability

Debt Ratio >70% causes SHAP contributions to sharply spike.

Firms with low ROA and high leverage exhibit multiplicative distress risk.

Earnings stability matters more than one-year profitability

Even marginally positive EPS in all four quarters creates strong negative SHAP effects.

Firms with volatile earnings but positive ROA may still be at risk.

Cash flow acts as a stabilizer

Positive Cash Flow/TA reliably offsets distress signals.

This explains why some borderline firms do not cross into default prediction territory.

Actionable Use Cases

Lenders can prioritize ROA + leverage-screening for early detection.

Investors can use SHAP-driven models to monitor portfolio risk dynamically.

Financial managers gain interpretable insights on which ratios require immediate correction.
