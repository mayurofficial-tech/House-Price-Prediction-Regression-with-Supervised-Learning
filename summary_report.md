# Summary Report: House Price Prediction

## Business Problem and Dataset

The goal of this project was to predict residential house sale prices
from property characteristics. Accurate price estimates can help
real-estate professionals create more consistent initial valuations,
compare properties, and identify homes that may be priced unusually high
or low. The project used the Ames Housing dataset, which contains
property-related information such as overall quality, living area,
basement space, garage capacity, and construction year, together with
the target variable `SalePrice`.

## Preprocessing and Feature Engineering

The target price was transformed using `log1p(SalePrice)`. House prices
are often right-skewed, and the log transformation can reduce the
influence of very expensive properties and help regression models learn
more stable patterns. Predictions were converted back to the original
USD scale with `expm1` when calculating business-facing error metrics.

The preprocessing workflow handled missing values through imputation so
that models could train without being disrupted by incomplete records.
Categorical variables were encoded into numeric representations, while
numerical features were scaled where appropriate for the model,
particularly for linear models with regularization. Preprocessing was
organized in a pipeline to keep transformations consistent between
training and test data and reduce data leakage risk. The project
compared Linear Regression, Ridge, Lasso, Random Forest, and XGBoost
using test-set metrics such as RMSE, MAE, and R², alongside
cross-validation where applicable.

## Model Performance

XGBoost was a strong candidate in the model comparison. Its five-fold
cross-validation RMSE on the log target was approximately **0.1226**,
with a standard deviation of **0.0091**; the test-set log-scale RMSE was
approximately **0.1176**. The closeness of these values suggests
reasonably consistent performance across the validation folds and
held-out test set. The final model choice should be confirmed against
the consolidated comparison table using original-USD RMSE and MAE, R²,
and training time. For a business deployment, error in dollars is
especially important because it is easier for agents and homeowners to
interpret.

## Predictive Features and Business Meaning

For the Ames Housing dataset, three commonly influential predictors to
verify against the model's actual feature-importance output are:

1.  **OverallQual:** The overall material and finish quality rating.
    Higher-quality homes may attract stronger offers and support higher
    asking prices.
2.  **GrLivArea:** Above-ground living area in square feet. More usable
    interior space can increase a property's appeal, although the effect
    depends on layout, location, and condition.
3.  **TotalBsmtSF:** Total basement area in square feet. Additional
    basement space can add utility and value, particularly when it is
    usable and well maintained.

These features describe model associations, not proof that changing one
characteristic alone will cause a specific price increase. The final
report should use the exact top three features produced by the fitted
model's importance analysis if they differ from these expected examples.

## Next Steps for Production

Next, I would validate the model on newer sales and, where possible,
across different neighborhoods and price bands. I would compare errors
by location and property type, inspect large residuals, and monitor data
drift after deployment. Hyperparameter tuning with Bayesian optimisation
could improve performance more efficiently than an exhaustive search. I
would also test a carefully validated ensemble of complementary models,
keep a simple baseline for comparison, and retrain periodically as
market conditions change. Finally, I would document model limitations
and present prediction ranges rather than a single price alone, so
professionals understand the uncertainty in each estimate.
