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

# Model Performance Analysis:
The model’s performance was assessed using several standard classification metrics, and the results show a clear difference between how well the model handles the majority class compared to the minority class. Since bankruptcy cases are rare, the key concern is how effectively the model identifies firms that are genuinely at risk rather than how well it performs overall.
1. Interpretation of the Performance Metrics
The confusion matrix indicates that the model correctly classified 1,285 non-bankrupt firms, with only 35 misclassified as bankrupt. More importantly, it identified 31 out of 44 actual bankruptcies, leaving 13 cases undetected. Although the dataset is highly imbalanced, the model still captures a substantial portion of the distressed firms.
The overall accuracy of 96% appears high, but in this context it is not the most meaningful measure because the majority class dominates the dataset. The more informative indicators are the class-specific metrics. For the bankrupt class, the model achieved a recall of 0.70, meaning it identified about 70% of the firms that genuinely failed. In applications involving financial distress, recall is especially important because missed bankruptcies can lead to significant financial losses.
The precision for the bankrupt class stands at 0.47, reflecting that just under half of the predicted bankruptcies were correct. While not ideal, this trade-off is typical when the model is tuned to prioritize recall. The F1-score of 0.56 summarizes the balance between precision and recall, and given the small number of positive cases, this outcome is reasonable.
The AUC score of 0.953 provides a broader view of the model’s discriminative ability. An AUC above 0.95 suggests that the model is highly effective at separating distressed firms from healthy ones across a range of classification thresholds, reinforcing the strong predictive structure captured during training.
2. Discussion of Optimal Hyperparameters
The hyperparameters selected through GridSearchCV illustrate how the model balances complexity, stability, and sensitivity to the minority class. The final model uses 400 estimators, which helps reduce variance and stabilizes predictions across different subsets of the data. A maximum depth of 10 prevents individual trees from becoming overly complex, limiting the risk of overfitting while still allowing enough depth to capture non-linear relationships common in financial ratios.
The parameters min_samples_split = 5 and min_samples_leaf = 2 add further constraints to the tree-growing process, ensuring that splits occur only when sufficient data are present. These controls help smooth the decision boundaries and reduce the model’s sensitivity to noise.
Finally, the use of class_weight = "balanced" directly addresses the dataset’s imbalance. Without this adjustment, the model would tend to overlook bankruptcy cases simply because they are uncommon. By redistributing the weights, the algorithm places greater emphasis on correctly identifying bankrupt firms, which explains the relatively strong recall achieved.

# 2. Global SHAP Summary Interpretation: Top 5 Influential Predictors
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
# Local Case Study Interpretations
Case 1 — Index 830
The SHAP explanation for this firm shows a consistent pattern: nearly all influential features push the prediction toward the non-distressed category. The strongest downward pressure comes from the profitability indicators, particularly the three ROA measures. Each of these has a relatively high observed value, and the SHAP plot illustrates that they lower the model’s risk assessment more than any other group of variables.
The operating and sales margin indicators reinforce this effect. Their negative SHAP values suggest that the firm’s revenue-generating activities are functioning efficiently, which the model interprets as a stabilizing financial sign. Leverage-related variables make smaller contributions, but they move in the same direction: the capital structure appears sustainable enough that it does not add any meaningful concern.
Taken together, the SHAP force plot for Case 1 depicts a firm whose profitability and margin performance outweigh all other considerations, leaving little room for features that would elevate risk. The model therefore places the company comfortably in the non-distressed category.
Case 2 — Index 498
In Case 2, the model again classifies the firm as low-risk, but the SHAP distribution is more balanced than in Case 1. Profitability indicators still provide the main downward pull on the predicted risk, but their contributions are somewhat smaller. The SHAP plot shows several features related to efficiency and working-capital management exerting mild positive pressures. While none of these is large enough to shift the prediction toward distress, they do slightly erode the strength of the profitability signals.
These positive contributions likely reflect operational frictions—possibly slower turnover or less efficient use of assets—compared with the previous case. Importantly, leverage indicators remain neutral or slightly protective, suggesting that the firm does not face structural solvency issues.
Overall, the SHAP pattern indicates a company that is fundamentally sound but not as consistently strong as the first case. Its profitability still dominates the explanation, but a handful of operational weaknesses prevent the model from giving an unqualified low-risk reading.
Case 3 — Index 81
Case 3 presents an even clearer picture of financial stability. The SHAP values show a strong cluster of negative contributions, with no major positive counterweights. Profitability, once again, is the decisive factor: the ROA measures and Net Income to Equity display particularly substantial downward impacts. These are complemented by operating margin indicators that reinforce the impression of a firm generating income effectively from its core activities.
Leverage variables play only a minor role but still contribute small negative values, indicating that the firm carries a manageable level of debt and does not face capital-structure pressures. There is little evidence of liquidity or efficiency issues in this observation, as reflected in the absence of meaningful positive SHAP contributions.
The overall explanation suggests that this firm combines strong earnings with stable leverage, resulting in a risk profile that is even more comfortably positioned in the non-distressed zone than the other two cases.
Synthesis Across All Three Cases
Across the three observations, the SHAP explanations highlight a consistent pattern. Profitability measures—especially the ROA series and income-to-equity ratio—play the dominant role in reducing predicted risk. Margin indicators further reinforce this effect. Where the cases differ is in the presence or absence of small positive contributions from efficiency-related variables. Only Case 2 shows any notable upward pressure, and even there it is mild. All three cases present stable leverage positions, which keeps solvency concerns minimal in the model’s assessment.

#Explaining Divergences Between Random Forest and SHAP Feature Importance
This section explains why the feature importance ranking produced by the Random Forest classifier differs from that generated by SHAP for the same model. Although both techniques aim to quantify how individual variables influence predictions, they do so through fundamentally different mechanisms. These methodological differences naturally lead to variations in the relative importance assigned to specific financial ratios in this bankruptcy‑prediction model.
Random Forest Feature Importance
Random Forests determine importance by measuring how much each feature reduces impurity across the ensemble of decision trees. Features that repeatedly appear in high‑level splits or create large reductions in Gini impurity accumulate higher scores. This method therefore tends to reward variables that act as efficient splitters, even if their actual effect on the predicted probability is modest. As a result, variables such as Net_Income_to_Total_Assets and Continuous_Interest_Rate_After_Tax rise to the top of the RF ranking because they frequently participate in early branching decisions.
SHAP Feature Importance
In contrast, SHAP importance is derived from the average magnitude of SHAP values across all observations. Rather than focusing on how features influence tree structure, SHAP measures how much each variable shifts the model’s prediction relative to a baseline. This makes SHAP more sensitive to the actual quantitative influence of a feature on individual predictions, including non‑linear patterns and interactions. Consequently, features such as Persistent_EPS_Last_4_Seasons and Borrowing_Dependency appear more prominently in the SHAP ranking because they consistently alter predicted risk across many samples, even if they do not create the largest impurity reductions in the forest.
Reasons for the Divergence
Several factors explain the differences between the two rankings in this model run:
1. Different definitions of “importance.”
The Random Forest approach rewards structural usefulness in tree construction, whereas SHAP focuses on the actual impact on predicted probabilities.
2. Sensitivity to correlated features.
When variables are correlated, Random Forests often assign most of the importance to whichever feature the algorithm selects first for splitting. SHAP distributes influence more evenly across correlated predictors, which can lower the RF‑dominant feature’s SHAP score.
3. Role of interaction effects.
Random Forest importance does not explicitly account for interactions; SHAP incorporates them by evaluating feature contributions across many coalition combinations. This makes SHAP more reflective of the true influence of variables whose effect depends on other financial indicators.
4. Local versus global influence.
RF importance is a fully global measure summarizing impurity reductions across the entire ensemble. SHAP aggregates local, observation‑level effects, capturing the variability in how features matter for different firms.
Conclusion
The differences between the RF and SHAP importance rankings are therefore expected and arise from the contrasting principles behind the two methods. RF highlights variables that structure the decision trees effectively, while SHAP identifies the features that genuinely shape prediction outcomes. In financial distress modelling, where variables are often correlated and interact in non‑linear ways, SHAP provides a more transparent view of how the model arrives at its risk assessments.
