<p align="center">
  <img src="assets/blueprint_header.svg" alt="House Price Prediction Using Machine Learning" width="100%" />
</p>

<p align="center">
  <a href="PASTE_YOUR_VIDEO_LINK_HERE"><b>🎬 &nbsp;WATCH THE PROJECT WALKTHROUGH</b></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white" />
  <img src="https://img.shields.io/badge/XGBoost-189AB4?style=for-the-badge" />
  <img src="https://img.shields.io/badge/pandas-150458?style=for-the-badge&logo=pandas&logoColor=white" />
  <img src="https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white" />
</p>

---

## 📐 TITLE BLOCK

```text
┌─────────────────────────────────────────────────────────────┐
│  PROJECT    :  House Price Prediction Using ML              │
│  DATASET    :  Ames Housing  (data/train.csv)               │
│  TARGET     :  SalePrice  (modelled as log1p)               │
│  TASK       :  Supervised Learning · Regression             │
│  MODELS     :  5 compared                                   │
│  TOOLS      :  Python · scikit-learn · XGBoost · SHAP       │
│  DRAWN BY   :  Mayur Makwana                                │
└─────────────────────────────────────────────────────────────┘
```

## 📑 DRAWING INDEX

| Sheet | Section | Sheet | Section |
|:-:|---|:-:|---|
| **01** | [Project Overview](#sheet-01--project-overview) | **07** | [Business Interpretation](#sheet-07--business-interpretation) |
| **02** | [Business Problem](#sheet-02--business-problem) | **08** | [Technologies](#sheet-08--technologies) |
| **03** | [Dataset](#sheet-03--dataset) | **09** | [How to Run](#sheet-09--how-to-run) |
| **04** | [Workflow](#sheet-04--workflow) | **10** | [Future Improvements](#sheet-10--future-improvements) |
| **05** | [Models Compared](#sheet-05--models-compared) | **11** | [Repository Structure](#sheet-11--repository-structure) |
| **06** | [Evaluation](#sheet-06--evaluation) | | |

---

## SHEET 01 · PROJECT OVERVIEW

A machine-learning regression project that predicts **residential house sale prices** from property characteristics. The workflow compares baseline and ensemble models, evaluates prediction errors, and interprets influential features to support real-estate decision-making.

The objective is to estimate a home's sale price from available property information, following a reproducible workflow:

`Data inspection` → `Preprocessing` → `Feature preparation` → `Model training` → `Evaluation` → `Residual diagnostics` → `Feature interpretation`

---

## SHEET 02 · BUSINESS PROBLEM

House prices depend on many factors, including overall quality, living area, basement space, garage capacity, and construction year. Manual estimates can vary between professionals. A predictive model can provide a **consistent starting estimate** to help real-estate professionals compare properties and support pricing discussions.

> [!IMPORTANT]
> Model predictions are **decision support**, not a replacement for professional valuation.

---

## SHEET 03 · DATASET

This project uses the **Ames Housing** dataset (`data/train.csv`), which contains residential property attributes and the target variable `SalePrice`.

| Feature group | Examples |
|---|---|
| 🏅 **Quality & condition** | Overall material and finish quality, property condition |
| 📏 **Size & space** | Above-ground living area, basement area |
| 🚗 **Property amenities** | Garage capacity and other facilities |
| 🏗️ **Age & location** | Construction year, neighborhood-related information |

---

## SHEET 04 · WORKFLOW

```text
 ① EDA
    Inspect columns, data types, distributions, missing values,
    and relationships with sale price
          ↓
 ② PREPROCESSING
    Impute missing values · encode categorical features ·
    scale numerical features where appropriate
          ↓
 ③ TARGET TRANSFORMATION
    log1p(SalePrice) to reduce right-skew
    expm1(prediction) to return to USD scale
          ↓
 ④ PIPELINE CONSTRUCTION
    Preprocessing + model together → consistent transformations,
    helps prevent data leakage
          ↓
 ⑤ TRAINING & COMPARISON
    Multiple regression algorithms, same train/test split
          ↓
 ⑥ EVALUATION
    RMSE · MAE · R² · CV RMSE (where applicable) · training time
          ↓
 ⑦ DIAGNOSTICS & INTERPRETATION
    Residual plots · feature importance · optional SHAP
```

---

## SHEET 05 · MODELS COMPARED

| Model | Family |
|---|---|
| Linear Regression | Linear (baseline) |
| Ridge Regression | Linear (regularised) |
| Lasso Regression | Linear (regularised) |
| Random Forest Regressor | Tree ensemble |
| XGBoost Regressor | Gradient boosting |

The best model is selected from the consolidated evaluation table, prioritizing **held-out performance** and **consistency across cross-validation**, not training performance alone. The selected model is saved in `model/house_price_model`.

---

## SHEET 06 · EVALUATION

Predictions are evaluated on both the **transformed target scale** and the **original sale-price scale**. Business-facing RMSE and MAE are reported in USD after applying `expm1` to predictions and transformed targets. R² indicates the proportion of target variance explained on the evaluated scale.

**XGBoost result recorded during development**

| Metric | Scale | Value |
|---|---|---|
| Cross-validation RMSE | log-target | ≈ **0.1226 ± 0.0091** |
| Test RMSE | log-target | ≈ **0.1176** |

> [!NOTE]
> These are **log-scale metrics, not dollar errors.** USD-scale RMSE and MAE come from the final comparison table.

---

## SHEET 07 · BUSINESS INTERPRETATION

Feature importance shows which property characteristics the fitted model relies on most. Commonly influential Ames Housing features include:

| Feature | Meaning |
|---|---|
| `OverallQual` | Overall material and finish quality |
| `GrLivArea` | Above-ground living area |
| `TotalBsmtSF` | Total basement area |

> These are examples to verify against the actual model output. Importance reflects **predictive association, not causation**, and does not guarantee that changing a feature will produce a particular price change. SHAP can add information about the direction and size of each feature's contribution.

---

## SHEET 08 · TECHNOLOGIES

`Python` · `pandas` · `NumPy` · `Matplotlib` · `Seaborn` · `scikit-learn` · `XGBoost` · `SHAP (optional)` · `Jupyter Notebook`

---

## SHEET 09 · HOW TO RUN

**1️⃣ Clone or download this repository**

**2️⃣ Create and activate a virtual environment** *(recommended)*

```bash
python -m venv .venv

# Windows
.venv\Scripts\activate

# macOS / Linux
source .venv/bin/activate
```

**3️⃣ Install the required packages**

```bash
pip install -r requirements.txt
```

No `requirements.txt` handy? Install the main packages directly:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost shap jupyter
```

**4️⃣ Check the dataset location**

The notebook expects the dataset at `data/train.csv`. If you keep it elsewhere, update the path in the notebook.

**5️⃣ Open and run the notebook from top to bottom**

```bash
jupyter notebook notebook/HousePrice_SupervisedLearning.ipynb
```

**6️⃣ Verify the notebook settings**

Check that the data paths, target column, preprocessing pipeline, and model step names match your environment.

---

## SHEET 10 · FUTURE IMPROVEMENTS

- 🔹 Collect newer sales data and validate on later transactions
- 🔹 Tune hyperparameters using Bayesian optimisation or a carefully designed search
- 🔹 Test stacking or blending only if cross-validation shows a reliable improvement
- 🔹 Analyse errors across neighborhoods and price ranges
- 🔹 Monitor data drift and retrain when market conditions change
- 🔹 Provide prediction intervals or uncertainty estimates alongside point predictions

---

## SHEET 11 · REPOSITORY STRUCTURE

```text
📐 house-price-prediction/
 ├─ 📁 assets/
 │   └─ 🎞️ blueprint_header.svg
 ├─ 📁 data/
 │   └─ 📊 train.csv
 ├─ 📁 model/
 │   └─ 🧠 house_price_model
 ├─ 📁 notebook/
 │   └─ 📓 HousePrice_SupervisedLearning.ipynb
 ├─ 📄 .gitignore
 ├─ 📄 README.md
 ├─ 📄 requirements.txt
 └─ 📄 summary_report.md
```

---

<p align="center">
  <b>✍️ DRAWN BY</b><br>
  <b>Mayur Makwana</b><br>
  <a href="https://github.com/mayurofficial-tech">GitHub</a>
  &nbsp;·&nbsp;
  <a href="YOUR_LINKEDIN_PROFILE_LINK_HERE">LinkedIn</a>
</p>