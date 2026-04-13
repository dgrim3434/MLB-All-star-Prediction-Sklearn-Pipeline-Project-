# MLB All-Star Prediction (Sklearn Pipeline Project)

## Overview

This project explores how accurately MLB All-Star selections can be predicted using **first-half season player statistics**.

The goal is to simulate real-world selection conditions by restricting features to **pre–All-Star break performance**, rather than full-season data. This introduces a more realistic prediction challenge and avoids using information that would not have been available at the time of selection.

This project is part of a **52-week machine learning capstone series**, with this week focused on **building end-to-end modeling pipelines using scikit-learn**.

---

## Problem Definition

The task is framed as a **binary classification problem**:

- **1** → Player selected to the All-Star Game  
- **0** → Player not selected  

The objective is to evaluate how well statistical performance alone can explain All-Star selections, while acknowledging that real-world selection also includes subjective factors such as popularity and fan voting.

---

## Data Sources

- **FanGraphs Player Statistics (2015–2019)**  
  - Exported via FanGraphs subscription  
  - Includes hitter performance metrics (e.g., WAR, OPS, SLG, AVG, HR)  
  - Filtered to include only **pre–All-Star break statistics**

- **All-Star Rosters (2015–2019)**  
  - Scraped from Wikipedia using a custom script  
  - Used to construct the target variable for classification  

Due to the absence of a shared unique identifier, datasets were joined using **(player name, team, year)** after normalization.

---

## Modeling Approach

- Models evaluated:
  - Logistic Regression  
  - Random Forest  
  - Gradient Boosting  

- **Evaluation Metric:** F1-score (to handle class imbalance)

- **Training Strategy:**
  - Trained on 2015–2018 data  
  - Evaluated using **stratified cross-validation**  
  - Final evaluation performed on a **2019 holdout test set**

- **Final Model:**
  - Random Forest  
  - Selected due to the highest cross-validated F1-score and ability to capture non-linear relationships  

---

## Results

### Test Set Performance (2019)

| Class        | Precision | Recall | F1-Score |
|-------------|----------|--------|----------|
| Non All-Star | 0.90     | 0.84   | 0.87     |
| All-Star     | 0.60     | 0.72   | 0.65     |

- **ROC AUC:** 0.852  

The model performs well at identifying non-All-Star players and shows moderate success in identifying All-Star selections despite class imbalance.

---

## Key Insights

- The most important features were:
  - **WAR (Wins Above Replacement)**
  - **Runs (R)**
  - **Slugging Percentage (SLG)**  

- The model relies heavily on **overall offensive production and cumulative value metrics**, suggesting that All-Star selections are strongly driven by total performance rather than isolated efficiency metrics.

---

## Limitations

This project intentionally reflects real-world data constraints, and several limitations should be noted:

- **No positional data**
  - Different positions prioritize different statistics (e.g., offensive vs defensive value)

- **Imperfect data join**
  - Matching was based on name/team/year due to lack of unique identifiers

- **No popularity or voting factors**
  - Fan voting, reputation, and prior selections are not captured

These factors likely contribute to the gap between model predictions and actual selections.

---

## Project Context

This is **Week 12 of a 52-week machine learning capstone series**, focused on:

- Building **scikit-learn pipelines**
- Understanding **model comparison and evaluation**
- Applying ML to **real-world, imperfect datasets**

---

## Tech Stack

- Python  
- Pandas / NumPy  
- Scikit-learn  
- Matplotlib / Seaborn  

---

## Takeaway

This project demonstrates how far **statistical performance alone** can go in predicting All-Star selections, while also highlighting the limitations of purely data-driven approaches in domains influenced by subjective decision-making.
