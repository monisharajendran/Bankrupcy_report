
1. Executive Summary
This study investigates the financial drivers of corporate distress using the Taiwanese Bankruptcy Prediction dataset. A Random Forest classifier, tuned through grid search and supported by SHAP explainability, was used to identify the indicators most strongly associated with bankruptcy outcomes. The model showed strong discriminative ability (AUC = 0.953) and succeeded in identifying the majority of distressed firms despite the substantial class imbalance in the data.
Across the global and local SHAP analyses, four themes consistently emerged as central predictors of financial distress:
•	Deteriorating profitability
•	Weak earnings persistence
•	Elevated leverage levels
•	Declining long term equity value
These patterns align with established theories of corporate failure, reinforcing the financial soundness of the model.

2. Model Performance Analysis
2.1 Interpretation of Classification Results
The confusion matrix shows the model correctly classified 1,285 non bankrupt and 31 bankrupt firms, misclassifying 35 non bankrupt and 13 bankrupt firms. Given the rarity of positive cases, the key concern is the model’s ability to detect actual bankruptcies:
•	Recall (bankrupt class): 0.70
The model identifies 70% of actual bankruptcies   an essential attribute in distress prediction, where missed defaults are costly.
•	Precision (bankrupt class): 0.47
Nearly half of the firms flagged as distressed were correctly identified. The drop in precision is expected when a model is tuned to favour recall in imbalanced datasets.
•	F1 score (bankrupt class): 0.56
Reasonable for a dataset where only ~3% of firms are bankrupt.
•	AUC: 0.953
Indicates excellent separation between distressed and healthy firms across threshold settings.
Overall, the model performs reliably for early warning purposes, prioritizing sensitivity to distress signals.
2.2 Optimal Hyperparameters and Their Effects
The chosen hyperparameters reflect a balance between model complexity and generalisation:
•	n estimators = 400 stabilises predictions across trees.
•	max depth = 10 prevents overfitting while capturing meaningful non linearities among financial variables.
•	min samples split = 5 and min samples leaf = 2 enforce smoother decision boundaries.
•	class weight = “balanced” ensures the minority class receives proportionate influence.
Collectively, these decisions contribute directly to the strong recall and AUC achieved.

3. Global SHAP Summary: Top Five Predictors
The global SHAP results reveal that the model relies primarily on financial variables describing profitability, earnings behaviour, leverage, and value growth.
1. ROA(C) – Before Interest and Depreciation
A consistently dominant predictor. Firms with low or negative ROA(C) showed strong positive SHAP values, pushing predictions toward bankruptcy.
2. Persistent EPS (Last 4 Seasons)
Highly unstable or negative EPS contributed materially to distress predictions, highlighting the importance of earnings sustainability rather than isolated quarterly outcomes.
3. Debt Ratio (%)
High leverage had a strong upward effect on predicted distress, reinforcing solvency risk as a structural driver of failure.
4. Net Value Growth Rate
Negative shareholder value growth signalled deeper performance issues, influencing long term solvency expectations.
5. Operating Profit Rate
Weak operating margins increased predicted distress by signalling declining operational competitiveness.
Summary:
These predictors collectively emphasize the importance of profitability quality, earnings stability, debt structure, and long term value creation in shaping the model’s assessment of financial health.

4. Local Case SHAP Explanations
Unlike generic summaries, the following interpretations reference the actual SHAP contribution patterns for indices 830, 498, and 81.
Case 1   Index 830
The SHAP values show that nearly all influential features push the model toward a low risk classification. ROA measures provide the strongest downward contribution, indicating robust core profitability. Operating margin components reinforce this effect. Leverage related indicators exert minimal influence, reflecting a manageable capital structure.
Overall: strong profitability and efficient operations dominate the explanation, with virtually no features pushing risk upward.

Case 2   Index 498
This case shows a more mixed pattern than Case 1. Profitability remains protective, but unlike Case 1, several working capital and operational efficiency features apply mild positive SHAP contributions. These reflect modest weaknesses such as slower turnover or slightly strained operating efficiency that dampen the strength of the profitability signals.
Overall: still a healthy firm, but with operational frictions that slightly elevate risk compared with Case 1.

Case 3   Index 81
Case 3 presents the clearest low risk profile. Profitability indicators such as Net Income to Equity and ROA dominate, pushing the prediction strongly toward non distressed. Unlike Case 2, there are virtually no upward pulling features. Leverage remains neutral to slightly protective, indicating a sustainable debt position.
Overall: strong earnings quality and stable capital structure produce a clean downward SHAP pattern.

Cross Case Synthesis
A consistent theme across all three cases is the dominant role of profitability in reducing distress risk. Operational margins support this effect. Only Case 2 shows notable positive SHAP contributions, indicating that efficiency pressures can moderate otherwise strong performance. Leverage plays a small but generally stabilizing role in all three.

5. Explaining Divergences Between RF Importance and SHAP Importance
Random Forest and SHAP produce different feature rankings because they measure fundamentally different aspects of importance:
1. Mechanism of Measurement
•	RF importance rewards features that reduce impurity during tree splits.
•	SHAP importance measures average magnitude of contribution to prediction shifts.
2. Sensitivity to Correlation
Correlated variables compete for importance in RF, often causing one to dominate. SHAP distributes contribution more evenly.
3. Interaction Effects
Random Forests do not explicitly quantify feature interactions; SHAP incorporates them through coalition values.
4. Local vs Global Perspectives
RF importance is purely global; SHAP aggregates local behaviour across all observations.
Implication for This Model
Features such as Net Income to Total Assets appear highly important in RF because they frequently appear early in tree splits, whereas SHAP elevates earnings persistence and borrowing dependency because these consistently shift predictions across many firms.

