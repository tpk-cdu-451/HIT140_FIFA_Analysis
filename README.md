# FIFA World Cup 2026 — Statistical Analysis & Match Outcome Modeling

**Unit:** HIT140 — Foundation of DataScience  
**Project:** Group Analytics Assessment (FIFA World Cup 2026)  
**Contributors:** Karma Choden | Mohith Suggala | Nikhitha Karne | Tejas Koradiya

---

## Summary

This repository contains statistical analysis, hypothesis testing, and pre-match linear regression models built on the FIFA World Cup 2026 tournament datasets. The project explores team disciplinary trends, goalkeeper impact across tournament stages, game control baselines, player shooting performance, and predictive outcome modeling.

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

Each task investigates a distinct focal question using data wrangling, descriptive analysis, 95% confidence intervals, and hypothesis testing.

| Task | Focal Investigation Question | Metric / Variable | Statistical Test | 
| :--- | :--- | :--- | :--- |
| **1. Disciplinary Trends** | Does the rate of cards (Yellow & Red) received per foul differ significantly between losing and winning teams? | Cards per foul ratio ($\text{Cards} / \text{Fouls}$) | **Two-Sample t-Test** (Independent) |
| **2. Goalkeeping Impact** | How do goals conceded against goalkeepers vary across teams, and do they significantly distinguish teams reaching the knockout stages? | Goals conceded per 90 minutes | **Two-Sample t-Test** (Independent) |
| **3. Possession Baseline** | What was the average ball possession percentage across tournament teams, and was it significantly different from the 50% benchmark? | Match possession share (%) | **One-Sample t-Test** ($\mu_0 = 50\%$) |
| **4. Attacking Output** | How do shooting opportunities and shooting accuracy influence goal scoring across player positions (Forwards vs. Midfielders)? | Shot conversion & goals per attempt | **Two-Sample t-Test** (Independent) |

---

## Objective 2: Pre-Match Linear Regression Modeling

All explanatory variables satisfy the pre-match availability requirement (collected strictly prior to match kickoff). Across both models, feature sharing is strictly limited to $\le 4$ variables.

### 2.1 Match Goal Difference Model ($N = 104$ Matches)
* **Target Variable ($Y$):** Match Goal Difference ($\text{Goals}_{\text{Team A}} - \text{Goals}_{\text{Team B}}$)
* **Dataset Scope:** 104 tournament matches

| Feature ID | Explanatory Variable ($X$) | Unit | Source |
| :--- | :--- | :--- | :--- |
| **Var 1** | `Squad_Market_Value_Diff_EUR_M` | EUR Millions | Transfermarkt |
| **Var 2** | `FIFA_Points_Diff` | Points | FIFA Official |
| **Var 3** | `Top5_League_Share_Diff_Pct` | Percentage (%) | FBref |
| **Var 4** | `Qualifying_Goal_Margin_Diff` | Goals / Match | FBref |
| **Var 5** | `Squad_Caps_Diff` | International Caps | FIFA Official |
| **Var 6** | `Avg_Squad_Age_Diff` | Years | FIFA Official |
| **Var 7** | `Confederation_Tier_Diff` | Tier Index | FIFA Official |
| **Var 8** | `Match_Stakes_Index` | Scale (1–10) | The Stats Don't Lie |

* **Model Diagnostics & Evaluation:**  
  * $R^2$: *TBD*  
  * Adjusted $R^2$: *TBD*  
  * RMSE: *TBD*  
  * MAE: *TBD*  

---

### 2.2 Team Goals Scored Model ($N = 208$ Observations)
* **Target Variable ($Y$):** Number of Goals Scored by a single team in a match
* **Dataset Scope:** 208 team-level match observations (2 per match)

| Feature ID | Explanatory Variable ($X$) | Unit | Source | Overlap with 2.1 |
| :--- | :--- | :--- | :--- | :---: |
| **Var 1** | `Team_FIFA_Points` | Points | FIFA Official | Yes |
| **Var 2** | `Opp_FIFA_Points` | Points | FIFA Official | Yes |
| **Var 3** | `Team_GF_Last5` | Scale (1–10) | The Stats Don't Lie | **Yes (1/4)** |
| **Var 4** | `Team_Qualifying_Goals_Per_Game` | Goals / Match | FBref | No |
| **Var 5** | `Squad_Career_Intl_Goals` | Goals | FIFA Official | No |
| **Var 6** | `Manager_Tenure_Years` | Years | Transfermarkt | No |
| **Var 7** | `Qualifying_Clean_Sheet_Rate` | Ratio (0–1) | The Stats Don't Lie | No |
| **Var 8** | `Avg_Height_CM` | Centimeters | FIFA Official | No |

* **Model Diagnostics & Evaluation:**  
  * $R^2$: *TBD*  
  * Adjusted $R^2$: *TBD*  
  * RMSE: *TBD*  
  * MAE: *TBD*  

---

## Getting Started

### Prerequisites & Dependencies
Run the project in Python 3.10+ with the following packages:
```bash
pip install pandas numpy scipy statsmodels scikit-learn matplotlib seaborn openpyxl
```

### Reproducing the Analysis
1. Clone the repository:
   ```bash
   git clone https://github.com/<your-username>/<repo-name>.git
   cd <repo-name>
   ```
2. Open and run the individual notebooks inside `Analysis_files/objective_1/` for inferential tests.
3. Open and run notebooks inside `Analysis_files/objective_2/` for regression fitting and evaluation metrics.
