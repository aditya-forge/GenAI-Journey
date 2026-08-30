# 🛠️ Machine Learning Practical — Lifecycle, Libraries & EDA

---

## 1. The Standard Machine Learning Lifecycle

```
 ┌─────────────────────┐
 │  1. Problem          │  Define goals, evaluation metrics, resource profile
 │     Definition        │
 └──────────┬───────────┘
            ▼
 ┌─────────────────────┐
 │  2. Data Collection   │  Company resources, web scraping, public datasets
 │     & Cleaning         │  → remove duplicates, handle missing values
 └──────────┬───────────┘
            ▼
 ┌─────────────────────┐
 │  3. Model Training    │  Route training data through algorithms to map
 │                       │  inputs → targets
 └──────────┬───────────┘
            ▼
 ┌─────────────────────┐
 │  4. Model Evaluation  │  Test on a strict holdout set to catch overfitting
 └──────────┬───────────┘
            ▼
 ┌─────────────────────┐
 │  5. Inference          │  Deploy the validated model into a live pipeline
 │     Deployment         │  to serve real predictions
 └──────────┬───────────┘
            ▼
      (loop back — retrain as fresh data/logs accumulate)
```

**Continuous optimization:** unlike static rule-based systems, ML pipelines are *loops* — accuracy keeps improving as new data arrives and the model is retrained.

---

## 2. Essential Python Libraries

| Library | Purpose | Snippet |
|---|---|---|
| **pandas** | Data manipulation via DataFrames — filtering, aggregation, time-series | `df = pd.DataFrame({'A':[1,2],'B':[3,4]})` |
| **NumPy** | Numerical computing, N-dimensional arrays | `arr = np.array([1,2,3]); arr*2` |
| **Matplotlib** | Static/interactive plots & charts | `plt.plot(x, y); plt.show()` |
| **Seaborn** | High-level statistical visualization (heatmaps, violin/box plots) | `sns.boxplot(data=[1,2,2,3,5])` |
| **Pickle** | Serialize/deserialize trained models to disk | `pickle.dump(data, open('model.pkl','wb'))` |

```python
import pandas as pd, numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import pickle

df = pd.DataFrame({'A': [1, 2], 'B': [3, 4]})
arr = np.array([1, 2, 3])
sns.set_theme()
sns.boxplot(data=[1, 2, 2, 3, 5])
```

---

## 3. Exploratory Data Analysis (EDA) — The 8-Step Framework

> EDA is a **mandatory** step before fitting any model — it inspects structure, detects anomalies, tests assumptions, and reveals correlations.

| # | Step | What it does |
|---|---|---|
| 1 | **Duplicates Handling** | Remove duplicate rows so they don't bias accuracy metrics |
| 2 | **Missing Values Imputation** | Choose a strategy: drop, flag, or impute (mean/median/mode) |
| 3 | **Label Encoding** | Convert categorical strings → numeric codes for distance-based models |
| 4 | **Outliers Handling** | Detect & handle extreme values, commonly via the **IQR method** |
| 5 | **Feature Selection** | Drop noisy/redundant columns to reduce dimensionality & overfitting |
| 6 | **Univariate Analysis** | Study **one** column at a time — histograms, box plots (spread, skew) |
| 7 | **Bivariate Analysis** | Compare **two** columns — scatter plots, correlation checks |
| 8 | **Multivariate Analysis** | Study relationships across **3+** columns simultaneously — hidden patterns |

### Quick memory hook

```
Duplicates → Missing → Encode → Outliers → Select
   → Univariate (1 col) → Bivariate (2 cols) → Multivariate (3+ cols)
```

---

## 📎 Lab Reference

- Interactive Notebook: *Core ML Modeling Building Practical*
- Dataset used: *Osteoporosis dataset*

---
*Source: SmartBridge/SkillWallet — "Machine Learning Practical: From ML Foundations to EDA"*
