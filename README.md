# UCSD 259 Practice and Applications

Final project for UC San Diego's DSC 259R (Data Science Practice and Applications). It analyzes Food.com recipes and user reviews (about 219,000 rated reviews) and builds a model that predicts whether a review gives 5 stars.

## Repository Contents

| File | Description |
|---|---|
| `final_project_submission.ipynb` | Full project: cleaning, EDA, missingness analysis, hypothesis testing and prediction models |

## Commit History

### `c4f6400`: Final project submission (2026-06-03)
- **Data cleaning and EDA:**
  - merged recipes with their reviews and dropped unneeded columns
  - added features such as total minutes, number of ingredients, and cook-time flags (≤15, ≤30 and ≤60 minutes)
  - univariate and bivariate plots with Plotly
  - group-bys and pivot tables
  - an analysis of reviews that modify the recipe
- **Missingness:**
  - ratings of 0 were treated as missing
  - permutation tests found that missing descriptions depend on the number of ingredients (p < 0.05)
- **Hypothesis testing:** found a statistically significant difference (p < 0.05), but the actual difference was tiny (~0.035) and not meaningful in practice.
- **Prediction problem:** a binary classifier for whether a review is 5 stars (77% of reviews are), with F1 as the main metric.
- **Baseline model:** logistic regression on recipe and review-length features. F1 = 0.663, accuracy = 0.550.
- **Final model:**
  - **Engineered features:** exclamation count, word count, sentiment, a recipe-modification flag, steps per ingredient, and TF-IDF on the review text.
  - **Compared four models with cross-validation:**

    | Model | Mean CV F1 |
    |---|---|
    | Logistic Regression | 0.912 |
    | Linear SVC | 0.911 |
    | Multinomial Naive Bayes | 0.901 |
    | Random Forest | 0.883 |

  - **Tuning:** `GridSearchCV` on logistic regression found the best settings: 5,000 TF-IDF features, 1–2 word phrases, and C = 0.5.
  - **Test set results:** F1 = **0.912** and accuracy = **0.858**, up from 0.663 and 0.550 for the baseline.

## Tools
Python, pandas, NumPy, scikit-learn, Plotly, Jupyter Notebook
