# National Data Science Competition — 1st Place

Winning solution for the National Data Science Competition (NDSC), predicting
college default rates from institutional and financial aid data. Built in R.

## Result

- **1st place nationally**
- Final model R² (test set): **0.885**

## Dataset

Four-year college data (admissions, cost, financial aid, outcomes) sourced from
[Skew The Script](https://skewthescript.org/s/four_year_colleges.csv).
80/20 train/test split, seed fixed for reproducibility.

## Approach

1. **Polynomial degree search** — for each numeric predictor, looped through
   polynomial degrees in `poly()` to find the degree that maximized R² when
   predicting `default_rate` individually.
2. **Transformations** — tested `log()` and `sqrt()` terms alongside polynomial
   terms.
3. **Interaction terms** — looped through all pairwise interactions between
   predictors (excluding non-predictive categoricals like name, city, state),
   keeping ones that improved R².
4. **Higher-order interactions** — extended the search to 3-way, then up to
   6-way interaction terms, adding any that improved fit.
5. **Pruning** — after each round of additions, iteratively removed terms that
   hurt R² (addressing overfitting from the large interaction search space).

This iterative add/prune cycle was repeated through 6-way interactions, after
which gains became marginal.

## Files

- `national_data_science_competition.ipynb` — full analysis, model search, and
  final model (see last cell for the final formula and R² calculation)

## Tech

- R (via Google Colab, `coursekata` package)
- Linear regression with `poly()`, interaction terms, stepwise feature pruning
