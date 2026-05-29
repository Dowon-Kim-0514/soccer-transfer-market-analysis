# Soccer Transfer Market Analysis

![R](https://img.shields.io/badge/R-276DC3?style=flat&logo=r&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat&logo=scikit-learn&logoColor=white)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=flat)

> Do xG-based performance metrics predict transfer fees in the Big 5 leagues?  
> Does the transfer market efficiently price player performance?

Predicting European football transfer fees using structural market variables, traditional performance statistics, and advanced metrics (xG, progressive carries, key passes) — across 1,407 transfers from the 2017–18 through 2023–24 seasons.

---

## Overview

This project examines whether football transfer fees can be predicted from a combination of:

- Structural market variables: age, contract status, league context, COVID timing
- Traditional football statistics: goals, assists, minutes played
- Advanced performance metrics: expected goals (xG), progressive carries, key passes, aerial win rate

The analysis focuses on transfers involving the Big 5 European leagues:

| League | Country |
|--------|---------|
| Premier League | England |
| La Liga | Spain |
| Bundesliga | Germany |
| Serie A | Italy |
| Ligue 1 | France |

---

## Research Questions

1. Do pre-transfer advanced metrics significantly predict transfer fees after controlling for structural variables?
2. Which better explains transfer-fee variation: traditional statistics or expectation-based metrics?
3. Do markets value players differently by position?
4. Are there league-level differences across the Big 5 in how player value is priced?
5. Do U21 players receive a conditional transfer premium?
6. Do O30 players receive a conditional veteran discount?

---

## Data Sources

- **FBref**: Big 5 player statistics accessed through `worldfootballR::load_fb_big5_advanced_season_stats()`
- **Transfermarkt**: Transfer records via Kaggle open dataset

The modeling sample includes 1,407 transfers for players with observable Big 5 pre-transfer performance histories.

---

## Methods

**Languages:** R (data collection, EDA, visualization, final report) + Python (ML modeling, residual analysis)

| Model | Variables | CV R² | Test R² |
|-------|-----------|-------|---------|
| Model 1 | Structural only | 0.210 | 0.270 |
| Model 2 | Model 1 + traditional metrics | 0.275 | 0.388 |
| Model 3 | Model 1 + advanced metrics | 0.280 | 0.333 |
| **Model 4** | **Combined (AIC/BIC + VIF selected)** | **0.378** | **0.468** |

The dependent variable is `log_transfer_fee`.

---

## Key Results

- The best-performing model was the final combined model (`Model 4`).
- `Model 4` achieved:
  - Test R-squared: `0.468`
  - Test RMSE: `0.926`
  - Cross-validated R-squared: `0.378` (SD: 0.045)
- Traditional metrics outperformed advanced metrics when each block was tested separately.
- Advanced metrics still added meaningful value when combined with traditional variables.
- Goals per 90 and xG per 90 both remained in the final model, suggesting the market rewards both realized output and underlying chance quality.
- Residual analysis showed that:
  - overall prediction errors were centered close to zero
  - goalkeeper valuation remained relatively noisy
  - U21 players showed a modest residual premium
  - league-level xG pricing sensitivity varied across the Big 5

---

## Repository Structure

```text
.
├── Final_Report_Master.Rmd
├── ML_Modeling_Cleaned.Rmd
├── README.md
├── data/
├── code/
├── EDA_figures/
└── kaggle_transfer_dataset/
```

Important files:

- `Final_Report_Master.Rmd`: final report source
- `ML_Modeling_Cleaned.Rmd`: modeling workflow
- `code/`: supporting scripts
- `data/`: cleaned and modeling-ready data
- `EDA_figures/`: exported exploratory figures

---

## How to Reproduce

1. Open `Final_Report_Master.Rmd` in RStudio.
2. Install the required R packages:
   - `knitr`, `readr`, `dplyr`, `tidyr`, `ggplot2`, `scales`, `patchwork`, `reticulate`
3. Update the `project_root` path to match your local machine.
4. Knit the report to PDF.

---

## Limitations

- Selection bias: players from outside the Big 5 excluded due to missing FBref coverage
- Observational study — results reflect associations, not causal effects
- SCA and Pressures unavailable in cached FBref pipeline
- Unobserved factors (agent influence, injury history, club finances) remain outside the dataset

---

## Final Deliverable

- `Soccer-Transfer-Market---Final-Report.pdf`

---

## Author

Dowon Kim  
UCLA Statistics & Data Science  
Personal portfolio project 2026 Spring
