# FIFA World Cup 2026 |  Statistical Analysis & Match Outcome Modeling


**Unit:** HIT140 — Foundation of DataScience  
**Project:** Group Analytics Assessment (FIFA World Cup 2026)  
**Contributors:** Karma Choden | Mohith Suggala | Nikhitha Karne | Tejas Koradiya

---
---

## Directory Structure
```text
├── Analysis_Files/
│   ├── objective_1/
│   │   ├── task1_cards_per_foul.ipynb
│   │   ├── task2_goalkeeper_performance.ipynb
│   │   ├── task3_ball_possession.ipynb
│   │   └── task4_shooting_efficiency.ipynb
│   └── objective_2/
│       ├── task2_1_goal_difference_regression.ipynb
│       └── task2_2_team_goals_regression.ipynb
├── raw_datasets/
└── README.md
```

---

## Data Sources

The project utilizes data sourced from verified public football databases:
* [FIFA Official Statistics](https://www.fifa.com/en/tournaments/mens/worldcup/canadamexicousa2026/statistics): Official match reports, squad demographics, caps, and confederation rankings.
* [FBref](https://fbref.com/en/): Detailed event logs, player-level performance metrics, and qualifying records.
* [The Stats Don't Lie](https://www.thestatsdontlie.com/football/world-cup-2026/): Tournament situational indexes, clean sheet ratios, and tactical indicators.
* [Transfermarkt](https://www.transfermarkt.com): Pre-tournament market valuations and managerial tenure.

---

## Objective 1: Exploratory & Inferential Statistics

# Summary

This repository contains statistical analysis, hypothesis testing, and pre-match linear regression models built on the FIFA World Cup 2026 tournament datasets. The project explores team disciplinary trends, goalkeeper impact across tournament stages, game control baselines, player shooting performance, and predictive outcome modeling.

Each task investigates a distinct focal question using data wrangling, descriptive analysis, 95% confidence intervals, and hypothesis testing.

| Task | Focal Investigation Question | Metric / Variable | Statistical Test | 
| :--- | :--- | :--- | :--- |
| **1. Disciplinary Trends** | Does the rate of cards (Yellow & Red) received per foul differ significantly between losing and winning teams? | Cards per foul ratio ($\text{Cards} / \text{Fouls}$) | **Two-Sample t-Test** (Independent) |
| **2. Goalkeeping Impact** | How do goals conceded against goalkeepers vary across teams, and do they significantly distinguish teams reaching the knockout stages? | Goals conceded per 90 minutes | **Two-Sample t-Test** (Independent) |
| **3. Possession Baseline** | What was the average ball possession percentage across tournament teams, and was it significantly different from the 50% benchmark? | Match possession share (%) | **One-Sample t-Test** ($\mu_0 = 50\%$) |
| **4. Attacking Output** | How do shooting opportunities and shooting accuracy influence goal scoring across player positions (Forwards vs. Midfielders)? | Shot conversion & goals per attempt | **Two-Sample t-Test** (Independent) |

---



## Objectives 2 

### Objective 2.1 — Predict Goal Difference
Predict the **goal difference between two opposing teams** using a dataset of **104 matches** and eight pre-match explanatory variables.

**Target:** `Goal_Difference` (Team A goals − Team B goals)

**Input features:**
1. `FIFA_Points_Diff`
2. `Squad_Age_Diff`
3. `Mean_Caps_Diff`
4. `Home_Country_Diff`
5. `Recent_GF_Diff`
6. `Recent_GA_Diff`
7. `Recent_FTS_Diff`
8. `Squad_Market_Value_Diff_EUR_M`

**Models compared:** Original Linear Regression, Yeo-Johnson + Linear Regression, Ridge, Huber, Random Forest, and Gradient Boosting.

**Selected model (five-fold cross-validation):** Original Linear Regression.

| Test metric | Result |
|---|---:|
| MAE | 1.034 |
| RMSE | 1.479 |
| R² | 0.382 |

### Objective 2.2 — Predict Team Goals
Predict the **number of goals scored by one team in a match** using **208 team-match observations** and eight pre-match explanatory variables.

**Target:** `Team_Goals`

**Input features:**
1. `Team_FIFA_Points`
2. `Opp_FIFA_Points`
3. `Team_GF_Last5`
4. `Opp_GA_Last5`
5. `Team_FTS_Rate_Last5`
6. `Opp_CS_Rate_Last5`
7. `Forecast_Temp_C`
8. `Knockout`

**Models compared:** Original Linear Regression, Yeo-Johnson + Linear Regression, Random Forest, Gradient Boosting, and Poisson Regression.

**Selected model (five-fold cross-validation):** Yeo-Johnson + Linear Regression.

| Test metric | Result |
|---|---:|
| MAE | 0.850 |
| RMSE | 1.185 |
| R² | 0.282 |

**Note:** Poisson Regression achieved the lowest test RMSE (1.133), but the model selection in the notebook was based on training-set cross-validation, which favoured Yeo-Johnson + Linear Regression.

## Methodology

1. **Data preparation:** Load Excel datasets, check required variables, and inspect data quality.
2. **Exploratory data analysis:** Examine descriptive statistics, distributions, and correlations.
3. **Train-test split:** Use 80% of data for training and 20% for testing (`random_state=42`).
4. **Cross-validation:** Use five-fold cross-validation to compare candidate regression models.
5. **Model evaluation:** Compare Mean Absolute Error (MAE), Root Mean Squared Error (RMSE), and R².
6. **Diagnostics:** Explore predictions, residual behaviour, and influential predictors.
7. **New predictions:** Use pre-match feature values to generate statistical predictions for a new fixture.

## Tools & Libraries

- **Python:** pandas, NumPy, Matplotlib, Seaborn
- **Machine learning:** scikit-learn
- **Statistics:** SciPy, statsmodels
- **Data files:** Microsoft Excel (`.xlsx`)
- **Notebooks:** Jupyter Notebook / Google Colab

## Files

| File | Description |
|---|---|
| `Dataset2.1.xlsx` | Data for Objective 2.1 (104 matches); includes a data-preparation notes sheet. |
| `Dataset2.2.xlsx` | Data for Objective 2.2 (208 team-match observations); includes an additional detail sheet. |
| `FIFA_LinearRegression_2_1_Final_Analysis.ipynb` | Goal-difference prediction and model evaluation. |
| `FIFA_LinearRegression2_2_Final.ipynb` | Team-goals prediction and model evaluation. |

*Update these filenames to match the exact filenames used in your GitHub repository.*

## How to Run

1. Download or clone this repository.
2. Install the required libraries:
   ```bash
   pip install pandas numpy matplotlib seaborn scipy statsmodels scikit-learn openpyxl notebook
   ```
3. Open either Jupyter notebook or upload it to Google Colab.
4. Place the relevant Excel dataset in the notebook's working folder.
5. Update the dataset path in the notebook (Objective 2.1 currently refers to `/content/Dataset2.1.xlsx`).
6. Run the notebook cells in order to reproduce the analysis.

## Key Takeaways

- Pre-match variables provide some useful predictive information, but exact scorelines remain difficult to forecast.
- Cross-validation helps select models without using the held-out test data for model selection.
- MAE, RMSE, R², and residual plots help assess model strengths and limitations.
- These results describe the uploaded datasets and notebook runs; the underlying match records and source provenance should be independently checked before claiming the dataset is officially verified.

## Limitations

- Predictions are estimates, not guaranteed match outcomes.
- The dataset is relatively small, especially for the 104-match goal-difference task.
- Objective 2.2 has two team observations per match; a random row-based split may place opposite sides of the same match in both training and test sets. A match-grouped split would provide a stronger assessment of performance on unseen matches.
