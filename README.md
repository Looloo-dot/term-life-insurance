# Term Life Insurance

This repository contains the empirical work for ME315 Problem Set Day 4, Question 3. The project studies household predictors of term life insurance coverage using the Term Life Insurance dataset from the 2004 Survey of Consumer Finances.

## Files

- `Q3 notebook.ipynb`: main Jupyter notebook for data inspection, feature engineering, regression modelling, robustness checks and classification extension.
- `Term Life Insurance.csv`: dataset used by the notebook.
- `term_life_q3_report.tex`: LaTeX source for the written report and appendix.
- `figures/figure1_distribution_model_comparison.png`: figure used in the report.
- `Appendix_Reproducibility_Draft.md`: earlier appendix planning notes.

## Reproducibility

Run the notebook from this repository folder so the relative data path works:

```python
pd.read_csv("Term Life Insurance.csv")
```

The analysis uses Python with `pandas`, `numpy`, `matplotlib`, `statsmodels` and `scikit-learn`. The main train/test split uses `random_state=123`; the repeated-split robustness check uses seeds 100 to 129.

## Main Empirical Design

The project treats term life insurance coverage as having two margins:

1. whether a household has positive coverage;
2. how large coverage is, conditional on positive coverage.

The main analysis models `log(FACE)` among households with `FACE > 0`. Ridge and Lasso are compared with an income-only benchmark and an interpretable OLS model using held-out RMSE and repeated train/test splits.
