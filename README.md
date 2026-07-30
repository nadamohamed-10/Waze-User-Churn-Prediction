# Waze User Churn Prediction

A capstone-style project for the Google Advanced Data Analytics Certificate. Waze
leadership asked the data team to build a machine learning model that predicts
monthly user churn, so the company can proactively retain at-risk users and
support growth.

> **Note:** The scenario, stakeholders, and dataset are fictitious and were
> created for pedagogical purposes. They do not represent Waze's actual data,
> employees, or business.

**Status: 🚧 in progress.** This is a living repo — I'm building it out course by
course as I go, so expect the modeling section to fill in over time. See
[Project status](#project-status) below for exactly what's done vs. planned.

## Project goal

Predict whether a Waze user will churn (uninstall or stop using the app) in a
given month, and surface the factors that drive churn so the team can design
targeted retention strategies.

## The dataset

`waze_dataset.csv` — 14,999 rows (one per user), 13 columns. 700 rows are
missing the churn label and are excluded from any churned-vs-retained
comparison.

| Column | Type | Description |
|---|---|---|
| `label` | str | Target: `retained` or `churned` |
| `sessions` | int | App opens during the month |
| `drives` | int | Drives (≥1 km) during the month |
| `device` | str | iPhone / Android |
| `total_sessions` | float | Modeled estimate of total sessions since onboarding |
| `n_days_after_onboarding` | int | Tenure, in days |
| `total_navigations_fav1` / `fav2` | int | Navigations to favorite places 1 / 2 |
| `driven_km_drives` | float | Total km driven during the month |
| `duration_minutes_drives` | float | Total minutes driven during the month |
| `activity_days` | int | Distinct days the app was opened |
| `driving_days` | int | Distinct days the user drove |

## Project status

| Stage | What it covers | Status |
|---|---|---|
| **Plan** | Project proposal, milestones, stakeholders | ✅ Done — [`docs/Waze_PACE_Project_Proposal.docx`](docs/Waze_PACE_Project_Proposal.docx) |
| **Analyze — EDA** | Cleaning, missing-value handling, box/scatter plots, churn-by-device | ✅ Done — [`notebooks/Waze_EDA_Course2.ipynb`](notebooks/Waze_EDA_Course2.ipynb) |
| **Analyze/Construct — Feature engineering** | 7 engineered features, 13 business-question-driven visualizations, churn-rate breakdowns by activity/engagement/distance | ✅ Done — [`notebooks/Waze_EDA_FeatureEngineering.ipynb`](notebooks/Waze_EDA_FeatureEngineering.ipynb) |
| **Construct — Hypothesis testing** | Statistical tests on key variable relationships | ⬜ Planned |
| **Construct — Modeling** | Train/evaluate churn classifiers (e.g., logistic regression, tree-based models), handle class imbalance, feature selection | ⬜ Planned |
| **Execute — Model evaluation** | Metrics against project requirements, error analysis | ⬜ Planned |
| **Execute — Communication** | Executive summary, stakeholder presentation | ✅ First pass done — [`docs/Waze_Executive_Summary.pptx`](docs/Waze_Executive_Summary.pptx) *(will be updated once modeling results land)* |

### Key EDA findings so far

- Overall churn rate is **~17.7%** among the 14,299 labeled users — a meaningful
  class imbalance to account for at modeling time.
- **Frequency of use beats volume of use** as a churn signal: churned users have
  a much lower median `activity_days` (8 vs. 17) and `driving_days` (6 vs. 14)
  than retained users, even though per-session driving intensity looks similar.
- `drives` and `sessions` are almost perfectly correlated (r ≈ 0.99) — likely
  redundant as independent model features.
- Churn rate is nearly identical across Android and iPhone — device type is not
  a useful churn predictor.
- A relatively small group of very high-usage users are captured by IQR outlier
  fences on `drives`/`sessions`/distance — likely genuine power users rather
  than bad data, and are capped (95th percentile) rather than dropped, in the
  feature-engineering notebook.


## Roadmap (what's coming next as I learn more ML)

- [ ] Hypothesis testing on key variable relationships (e.g., activity level vs. churn)
- [ ] Train/test split + baseline logistic regression classifier
- [ ] Tree-based models (random forest / XGBoost) and comparison against baseline
- [ ] Handle class imbalance (class weighting or resampling) and tune the
      decision threshold for the business use case
- [ ] Feature importance / interpretability (e.g., SHAP) to connect model
      output back to the EDA insights above
- [ ] Move reusable cleaning/feature-engineering code out of the notebooks and
      into `src/` as functions, once the pipeline stabilizes
- [ ] Update the executive summary with final model results and recommendations

