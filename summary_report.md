<p align="center">
  <img src="assets/blueprint_header.svg" alt="Summary Report: House Price Prediction" width="100%" />
</p>

<h1 align="center">📋 SUMMARY REPORT</h1>
<p align="center"><b>House Price Prediction</b> · Ames Housing · Regression</p>

---

## 📐 REPORT AT A GLANCE

| 🎯 Target | 🔁 Transform | 🤖 Models | 📉 CV RMSE (XGBoost) | 🧪 Test RMSE (XGBoost) |
|:-:|:-:|:-:|:-:|:-:|
| `SalePrice` | `log1p` | 5 compared | **0.1226** ± 0.0091 | **0.1176** |

> [!NOTE]
> The RMSE values above are on the **log-target scale**, not in dollars.

---

## 1️⃣ BUSINESS PROBLEM & DATASET

The goal of this project was to **predict residential house sale prices** from property characteristics.

Accurate price estimates help real-estate professionals to:

- 🔹 create more consistent initial valuations
- 🔹 compare properties
- 🔹 identify homes that may be priced unusually high or low

The project used the **Ames Housing** dataset, which contains property information such as overall quality, living area, basement space, garage capacity and construction year, together with the target variable `SalePrice`.

---

## 2️⃣ PREPROCESSING & FEATURE ENGINEERING

### 🔁 Target transformation

The target price was transformed using `log1p(SalePrice)`. House prices are often right-skewed, and the log transformation reduces the influence of very expensive properties and helps regression models learn more stable patterns. Predictions were converted back to the original USD scale with `expm1` when calculating business-facing error metrics.

### 🧹 Preprocessing pipeline

```text
  Raw data
     ↓
  Impute missing values        → models train without being disrupted
     ↓                           by incomplete records
  Encode categorical variables → numeric representations
     ↓
  Scale numerical features     → where appropriate, particularly for
     ↓                           regularised linear models
  Model fitting                → all inside one pipeline
```

Preprocessing was organised in a **pipeline** to keep transformations consistent between training and test data and to reduce data-leakage risk.

### 🤖 Models compared

`Linear Regression` · `Ridge` · `Lasso` · `Random Forest` · `XGBoost`

They were compared using test-set metrics (**RMSE, MAE, R²**), alongside cross-validation where applicable.

---

## 3️⃣ MODEL PERFORMANCE

XGBoost was a strong candidate in the model comparison.

```text
  XGBoost · RMSE on the log target

  5-fold CV   ████████████████████████  0.1226  (± 0.0091)
  Test set    ███████████████████████░  0.1176
```

The closeness of these values suggests **reasonably consistent performance** across the validation folds and the held-out test set.

> [!IMPORTANT]
> The final model choice is confirmed against the consolidated comparison table: original-USD RMSE and MAE, R², and training time. For a business deployment, **error in dollars matters most**, since it is easier for agents and homeowners to interpret.

---

## 4️⃣ PREDICTIVE FEATURES & BUSINESS MEANING

Three commonly influential predictors for Ames Housing, to be checked against the model's feature-importance output:

| # | Feature | Meaning | Business view |
|:-:|---|---|---|
| 1 | **`OverallQual`** | Overall material and finish quality rating | Higher-quality homes may attract stronger offers and support higher asking prices |
| 2 | **`GrLivArea`** | Above-ground living area (sq ft) | More usable space can raise appeal, though the effect depends on layout, location and condition |
| 3 | **`TotalBsmtSF`** | Total basement area (sq ft) | Extra basement space adds utility and value, especially when usable and well maintained |

> [!WARNING]
> These features describe **model associations, not proof of cause**. Changing one characteristic alone will not necessarily cause a specific price increase. If the fitted model's importance analysis ranks different features on top, those exact features are the ones to report.

---

## 5️⃣ NEXT STEPS FOR PRODUCTION

- [ ] **Validate** the model on newer sales, across different neighborhoods and price bands
- [ ] **Compare errors** by location and property type, and inspect large residuals
- [ ] **Monitor data drift** after deployment
- [ ] **Tune hyperparameters** with Bayesian optimisation, which can be more efficient than an exhaustive search
- [ ] **Test a validated ensemble** of complementary models, while keeping a simple baseline for comparison
- [ ] **Retrain periodically** as market conditions change
- [ ] **Document limitations** and present **prediction ranges** rather than a single price, so professionals understand the uncertainty in each estimate

---

<p align="center">
  <sub>📎 See the full project in <a href="README.md">README.md</a> · Notebook: <code>notebook/HousePrice_SupervisedLearning.ipynb</code></sub><br>
  <b>✍️ Mayur Makwana</b> · <a href="https://github.com/mayurofficial-tech">GitHub</a>
</p>