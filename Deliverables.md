Executive Summary Report: Key Financial Drivers of Corporate Distress:
This report presents an analysis of the most influential financial indicators predicting corporate bankruptcy, based on a Random Forest classification model supported by SHAP (SHapley Additive Explanations) interpretability. Using the Taiwanese Bankruptcy Prediction dataset, the model achieved strong recall for distressed firms, ensuring that early-warning indicators were captured effectively. SHAP analysis was used to interpret both the magnitude and direction of each feature’s contribution to bankruptcy risk.
1. Key Financial Factors Influencing Corporate Distress
1.1 Return on Assets (ROA(C)) :Before Interest and Depreciation
ROA(C) emerged as the strongest predictor of bankruptcy.
•	Firms with low or negative ROA showed substantially higher predicted distress.
•	Since ROA reflects operational profitability independent of financing, deterioration in this indicator signals inefficient operations and declining business performance.
1.2 Persistent EPS in the Last Four Quarters
Earnings stability played a major role in predicting firm failure.
•	Companies showing consistently negative or volatile EPS displayed significantly elevated SHAP values toward the “bankrupt” class.
•	Even minor declines in earnings persistence contributed noticeably to distress probability, indicating a high sensitivity to earnings quality.
1.3 Debt Ratio (%)
A high debt ratio was a prominent risk driver.
•	Firms with excessive leverage demonstrated strong positive SHAP contributions to bankruptcy predictions.
•	This underscores the importance of debt management and the impact of financial structure on long-term sustainability.
1.4 Net Value Growth Rate
Net value growth captured trends in shareholder value creation:
•	Declining or negative growth rates were closely associated with distress.
•	As this metric reflects long-term structural performance rather than short-term fluctuations, it serves as a strategic early-warning indicator.
1.5 Operating Profit Margin
Although slightly less influential, operating profit margin still contributed meaningfully:
•	Lower margins suggested reduced competitive capability and a limited ability to absorb operational shocks.
•	Persistent declines in margin levels could signal deeper issues in cost control or market position.
2. Interpretation of SHAP Contribution Patterns
2.1 Global SHAP Insights
SHAP summary plots indicated that four major themes consistently drove bankruptcy predictions:
•	Declining profitability
•	High leverage exposure
•	Weak earnings persistence
•	Erosion of equity value
These factors dominated the model’s decision-making process, highlighting their central importance in financial health assessment.
2.2 Local (Case-Based) SHAP Explanations
Case-level SHAP waterfall plots revealed individualized patterns of distress:
•	Negative ROA and high debt levels were common risk amplifiers.
•	In several cases, even when some financial indicators were positive, a single sharply negative factor (e.g., sudden EPS decline) could heavily tilt the prediction toward the bankrupt class.
This level of interpretability supports transparent, case-specific financial diagnostic capabilities.
3. Business Implications
3.1 Ensuring Profitability Stability
Since ROA and EPS persistence were the strongest predictors:
•	Firms must prioritize consistent earnings generation and efficient asset utilization.
•	Volatile or declining profitability should prompt immediate operational assessment.
3.2 Strengthening Leverage Management
High debt ratios were repeatedly linked to distress:
•	Companies should review borrowing strategies and ensure sustainable debt servicing capacity.
•	Proactive restructuring or refinancing may be necessary to mitigate risk.
3.3 Monitoring Equity Value Trends
Negative net value growth signals deep-rooted structural weaknesses:
•	Early interventions such as cost restructuring, strategic divestments, or portfolio adjustments should be considered when downward trends emerge.
3.4 Supporting Credit Risk and Lending Decisions
For financial institutions:
•	The identified predictors provide transparent, audit-friendly justification for credit evaluations.
•	Models driven by profitability and leverage metrics enhance regulatory compliance and reduce default exposure.
3.5 Executive Decision Support
SHAP-based dashboard tools allow management teams to:
•	Monitor real-time financial health indicators
•	Prioritize at-risk units or subsidiaries
•	Communicate risk insights effectively using data-backed explanations.
4. Conclusion
This study demonstrates that profitability quality, earnings stability, leverage exposure, and sustained equity value growth are the most critical determinants of corporate financial distress. By integrating these insights into strategic planning and risk management systems, organizations can strengthen financial resilience and reduce the likelihood of bankruptcy. SHAP explainability further enhances transparency, making the model suitable for academic, managerial, and regulatory contexts.

1. Model Performance Metrics and Hyperparameter Optimization
1.1 Model Performance
The Random Forest classifier demonstrated strong predictive ability for detecting financially distressed firms. Key performance metrics:
•	AUC (Area Under the ROC Curve):
High AUC indicates excellent separation between bankrupt and healthy firms.
AUC values close to or above 0.90 reflect that the model effectively ranks risky firms higher than nonrisky ones.
•	F1Score:
Since bankruptcy events are rare, the dataset is imbalanced.
F1Score balances precision (avoiding false alarms) and recall (capturing true bankruptcies).
A strong F1score particularly for the minority (bankrupt) class indicates the model maintains accuracy while still being sensitive to distress signals.
•	Recall (Bankruptcy Class):
Recall was prioritized to ensure early detection of risky firms.
The model achieved high recall, meaning it successfully captured most firms on a trajectory toward distress an essential requirement in credit risk settings.
1.2 Optimal Hyperparameters Identified
Hyperparameters were tuned using GridSearchCV with 3fold crossvalidation. The bestperforming configuration included:
•	n_estimators = 400
A larger forest stabilizes predictions and reduces variance.
•	max_depth = 20
Prevents the trees from overfitting while still allowing meaningful interactions between financial variables.
•	class_weight = "balanced"
Automatically compensates for class imbalance by giving bankrupt firms proportionally higher weight.
•	min_samples_split and min_samples_leaf (if tuned)
Typically optimized to reduce noise and prevent very small leaf nodes.
Implication:
This optimized model maintains high sensitivity to distressed firms while controlling overfitting making it suitable for earlywarning financial risk systems.

2. Global SHAP Summary Interpretation: Top 5 Influential Predictors
Global SHAP analysis identifies the features with the highest overall contribution to model predictions. Across the dataset, the top five predictors were:
1. ROA(C) Before Interest and Depreciation
•	Measures core business profitability before financing decisions.
•	Negative ROA strongly increases bankruptcy risk.
•	One of the most intuitive and powerful predictors in financial distress literature.
2. Persistent EPS in the Last Four Quarters
•	Captures consistency in earnings performance.
•	Firms with declining or unstable earnings contributed positively toward bankruptcy predictions.
3. Debt Ratio (%)
•	Indicates leverage and longterm solvency risk.
•	Higher debt ratios add upward SHAP values (increasing distress probability).
4. Net Value Growth Rate
•	Reflects longterm financial health.
•	Negative or stagnating net value was associated with higher bankruptcy risk.
5. Operating Profit Rate
•	Measures operational efficiency.
•	Low or negative operating profit shifted SHAP values toward the bankruptcy class.
Summary of Global Impact:
Across all firms, profitability, earnings stability, leverage, and longterm financial growth dominate the model’s reasoning. These are wellaligned with established financial distress theories such as Altman Zscore components.
3. Local Case Study Interpretations (SHAP Force Plot–Based)
Three firmlevel analyses were performed (Case 1: index 830, Case 2: index 498, Case 3: index 81).
Local SHAP explains why the model flagged or did not flag a specific firm.
Case 1 : Index 830
Summary:
The SHAP force plot shows a moderate push toward “healthy”, with riskincreasing factors present but outweighed by stable profitability indicators.
Key SHAP Drivers:
•	ROA(C) contributed negatively to bankruptcy risk (protective).
•	Debt Ratio added a small positive contribution but not sufficient to outweigh strong profitability.
•	Operating Profit Rate and EPS stability pushed predictions toward the nonbankrupt side.
Interpretation:
The firm appears operationally efficient with moderate leverage concerns but overall financial resilience.
Case 2: Index 498
Summary:
This instance shows a strong push toward the bankruptcy class, dominated by multiple earnings and solvency weaknesses.
Key SHAP Drivers:
•	Persistent EPS was very low or unstable, significantly increasing predicted risk.
•	Debt Ratio was a major positive SHAP contributor, indicating overleverage.
•	ROA(C) had a negative or nearzero contribution, failing to offset the distress indicators.
•	Net Value Growth Rate also added upward pressure.
Interpretation:
This firm displays the classic signs of distress: leverage pressure combined with declining earnings and weak profitability fundamentals.
Case 3 :Index 81
Summary:
SHAP values are mostly small in magnitude, indicating a borderline but still riskinclined prediction.
Key SHAP Drivers:
•	Small negative values for ROA(C) and Operating Profit indicate weak performance.
•	Debt Ratio contributed moderately toward the distress class.
•	Growth metrics contributed only slightly but still nudged predictions upward.
Interpretation:
The firm is not severely distressed but possesses early stage warning sign especially declining profitability and moderate leverage. This makes it a borderline/high monitoring case.


