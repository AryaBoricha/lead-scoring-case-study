# X Education: Lead Scoring Case Study

Logistic regression model that scores every lead from 0 to 100 so the sales team can focus on the leads most likely to convert.

## Problem
X Education sells online courses and receives many leads, but only about 38% convert. The goal was to build a model that gives each lead a score so the sales team can prioritise the most promising ones.

## Approach
- Dataset of 9,240 leads and 37 columns; overall conversion rate 38.54%
- Replaced "Select" placeholders with missing values, then dropped 7 columns with more than 40% missing data, 2 ID columns and 12 near-constant columns
- Created dummy variables for categorical columns and split the data 70/30 (6,468 train, 2,772 test)
- Scaled the numeric features
- Selected 15 features with RFE, then refined the model with statsmodels Logit using p-values and VIF, ending with 12 features (all VIF below 2)
- Chose a probability cutoff of 0.30 from the sensitivity, specificity and accuracy trade-off curve
- Converted probabilities into a 0-100 lead score: Hot (61-100), Warm (31-60) and Cold (0-30)

## Results (test set, cutoff 0.30)
| Metric | Value |
|---|---|
| Accuracy | 85.79% |
| Sensitivity | 78.56% |
| Specificity | 90.32% |
| Precision | 83.57% |

- Train AUC: 0.928
- Test leads by tier: 948 Hot, 55 Warm, 1,293 Cold
- For busy periods, a cutoff of about 0.40 gives roughly 85% precision with 76.9% sensitivity, so the sales team gets fewer but higher-quality leads

## Key drivers
- **Increase conversion likelihood:** Tags (Closed by Horizzon, Will revert after reading the email, Busy), leads from the Lead Add Form, working professionals, SMS sent as the last activity, the Welingak Website source and more time spent on the website
- **Decrease conversion likelihood:** Do Not Email = Yes and Olark Chat conversation as the last activity

## Limitation
Tags are recorded by the sales team after they contact a lead, so they can carry information about the outcome. A model that scores brand-new leads should leave them out.

## Tools
Python, pandas, NumPy, scikit-learn, statsmodels, matplotlib, seaborn

## Files
- `Lead_Scoring_Assignment_Python_ARYA_BORICHA.ipynb`: full analysis notebook
