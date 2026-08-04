# Unemployment Rate Analysis by Race, Gender, and Education

## Overview
This project explores how unemployment rates vary across race, gender, age group, education level, and industry using a simulated monthly labor market dataset (2023–2025). The goal was to identify which demographic and structural factors are the strongest predictors of unemployment, and whether disparities persist across groups after accounting for other factors.

**Note on data:** This dataset is simulated to reflect realistic labor market patterns, not raw government data. It was designed to approximate real-world dynamics (e.g., relative unemployment gaps by education and industry) for the purpose of this analysis.

## Research Questions
- Has the overall unemployment rate trended downward from 2023 to 2025, and is this pattern consistent across racial groups?
- Do unemployment trends differ for women by race between 2023 and 2025?
- Which demographic group — defined by race and age — experienced the largest percentage point change in unemployment between 2023 and 2025?

## Methodology
1. **Exploratory Data Analysis** — reviewed distributions, checked for missing values and duplicates, and visualized unemployment trends by race, gender, and education level.
2. **Feature Engineering** — encoded categorical variables (race, age group, education level, industry) using one-hot encoding; converted gender to a binary indicator.
3. **Modeling**
   - **Linear Regression** to predict unemployment rate and identify which features increase or decrease it, with 5-fold cross-validation to check stability.
   - **Random Forest Classifier** to predict whether a given demographic/industry segment falls above or below the median unemployment rate, evaluated with a confusion matrix, F1 score, and calibrated ROC-AUC.

## Key Findings

**Linear Regression:** R² = 0.86, RMSE = 1.32 (stable across 5-fold cross-validation, CV RMSE mean 1.32 ± 0.06)

| Increases unemployment | Decreases unemployment |
|---|---|
| Age 20–24 (+3.89 pts) | Bachelor's+ education (−2.63 pts) |
| Less than High School education (+2.82 pts) | Age 55+ (−1.52 pts) |
| Retail industry (+2.11 pts) | Age 45–54 (−1.28 pts) |
| Black race (+1.48 pts) | Technology industry (−1.14 pts) |
| Hispanic race (+0.60 pts) | White race (−1.05 pts) |

**Random Forest Classifier** (above vs. below median unemployment rate): F1 score = 0.98, calibrated ROC-AUC = 0.998

**Takeaway:** Education level and industry sector are the strongest overall predictors of unemployment rate, but clear racial disparities remain even after accounting for age, education, and industry — Black and Hispanic workers show meaningfully higher predicted unemployment than White workers with otherwise similar profiles.

## Tools Used
- Python (pandas, numpy)
- scikit-learn (Linear Regression, Random Forest, cross-validation, ROC-AUC, F1)
- matplotlib, seaborn (visualization)

## Files
- `notebooks/unemployment_analysis.ipynb` — full analysis notebook
- `data/unemployment_demographics_full.csv` — simulated dataset used in the analysis

## Possible Next Steps
- Test interaction effects (e.g., race × education)
- Analyze trends over time by group rather than in aggregate
- Validate patterns against real BLS/Census microdata
