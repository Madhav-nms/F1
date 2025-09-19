# Formula 1: Data Analysis and Podium Prediction 

<p align="center">
  <img src="2025_F1.jpg" alt="F1 Logo" width="750"/>
</p> 

## Executive Summary

Built a machine-learning pipeline on **multi-season F1 data** to predict **Top-3 podium finishes**. After cleaning/merging, the final feature table had **15,806 rows × 12 features**.  
On a held-out test set:

- **Logistic Regression** → **Accuracy: 0.80**, **Precision: 0.523**, **Recall: 0.854**, **F1 Score: 0.648**, **ROC-AUC: 0.889**  
- **Random Forest** → **Accuracy: 0.838**, **Precision: 0.647**, **Recall: 0.542**, **F1 Score: 0.590**, **ROC-AUC: 0.868**

**Trade-off:** Logistic Regression catches more true podiums (higher recall); Random Forest is stricter (higher precision). Insights emphasize **grid position** and **pit efficiency** as the biggest levers.

---

## Objective 

- **Predict** whether a driver finishes on the **podium (P1–P3)**.  
- **Explain** the factors that move podium probability the most.  
- **Translate** model outputs into **race-strategy ideas**.

--- 

## Data Overview

**Source:** [Formula 1 World Championship (1950 - 2024) ](https://www.kaggle.com/datasets/rohanrao/formula-1-world-championship-1950-2020)


Source tables loaded: **14 CSVs** (e.g., `results`, `races`, `drivers`, `constructors`, `circuits`, `pit_stops`, `qualifying`, `status`).  
Key row counts seen in the notebook:
- `results` **26,759 rows**  
- `pit_stops` **11,371 rows**  
- `qualifying` **10,494 rows**  
- Final merged/cleaned **15,806 rows**, **12 features**


Train / Test split (by race): **12,644 / 3,162**

**Target:** `podium = 1 if finish_position <= 3 else 0`

**Feature examples** (engineered & joined):
- `grid_position` (starting slot)  
- `num_pit_stops`, `avg_pit_ms` (pit-stop count & average time)  
- `best_qual_sec` (proxy for one-lap pace)  
- `year` (captures regulation/era effects)  
- `positions_gained` (finish − grid; negative → positions gained)

---

## Modeling & Results

Models:
- **Logistic Regression** (interpretable baseline)  
- **Random Forest** (non-linear interactions)

**Held-out test:**
- **Logistic Regression**  
  - Accuracy **0.801** · Precision **0.523** · Recall **0.854** · F1 **0.648** · ROC-AUC **0.889**
- **Random Forest**  
  - Accuracy **0.838** · Precision **0.647** · Recall **0.542** · F1 **0.590** · ROC-AUC **0.868**

**Interpretation:**  
- Use **LogReg** when you want to **maximize captures** of potential podiums (high recall).  
- Use **RF** when you need **fewer false positives** (higher precision) for conservative strategies.

---

## Key Insights

1. **Starting grid dominates** — front-row starters have much higher podium odds.  
2. **Pit efficiency matters** — **more stops** and **slower average pit times** reduce podium probability.  
3. **Qualifying pace translates** — faster `best_qual_sec` boosts podium chances.  
4. **Season/era effects (`year`)** — proxy for regulation cycles and team dominance; not causal by itself, but informative.  
5. **Positions gained** — consistent gainers convert more podiums **when other factors align**.

---

## Strategy Ideas (Turning insights into action)

- **Quali priority:** bias setup/tyres for one-lap pace to improve grid slot.  
- **Pit-lane excellence:** rehearse stops; aim to reduce **avg pit time** and avoid extra stops under SC/VSC.  
- **Threshold play:** from **P1–P4**, a cleaner **one-stop** (when tyre deg allows) often preserves podium odds.  
- **Risk bands:** use model outputs to tag **High / Medium / Low** podium probability and pick undercut/overcut tactics accordingly.

--- 

## Results (Quick Take)

**Test set:** 3,162 rows (split by race to avoid leakage)

| Model              | Accuracy | Precision (Podium) | Recall (Podium) | F1 (Podium) | ROC-AUC |
|--------------------|:-------:|:------------------:|:---------------:|:-----------:|:------:|
| Logistic Regression | 0.801   | 0.523              | **0.854**       | 0.648       | **0.889** |
| Random Forest       | **0.838** | **0.647**          | 0.542           | 0.590       | 0.868   |

**What this means**
- **LogReg** captures more true podiums (high recall) → good when missing a podium call is costly.  
- **Random Forest** is stricter (higher precision) → good when you want fewer false positives.  
- Across models, **grid position** and **pit efficiency** consistently drive podium outcomes.

**Decision guide**
- Optimize for **coverage** (find every potential podium): use **LogReg**, threshold ≈ **0.40–0.50**.  
- Optimize for **confidence** (call podiums only when likely): use **RF**, threshold ≈ **0.55–0.65**.

**Bottom line:** Podiums are set up on **Saturday (grid)** and protected in the **pit lane**.
