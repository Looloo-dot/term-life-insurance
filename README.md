# Household Predictors of Term Life Insurance Coverage

Which household characteristics predict how much term life insurance a household holds — and
does regularisation buy you anything over a transparent OLS model?

Uses the Term Life Insurance extract from the **2004 Survey of Consumer Finances** (500
households, 18 variables). The analysis is deliberately **predictive rather than causal**:
model comparison is done on held-out data, and OLS estimates are used to interpret direction
and magnitude rather than to claim identification.

## Empirical design

The outcome, `FACE` (policy payout), is awkward to model directly — it is **zero for 225 of
500 households** and heavily right-skewed among the 275 with positive coverage (median
10,000; upper quartile 200,000; maximum 14 million). The problem is therefore split into two
margins:

1. **Participation** — whether coverage is positive at all.
2. **Coverage size** — `log(FACE)` conditional on positive coverage. This is the main analysis.

Four specifications are compared: an income-only benchmark, an interpretable core OLS model
(log income, centred age and age², education, household size, gender, marital-status
dummies), and Extended Ridge and Lasso adding log total income, log charitable giving, and
ethnicity dummies.

Policy-side variables (`FACECVLIFEPOLICIES`, `CASHCVLIFEPOLICIES`, `BORROWCVLIFEPOL`) are
**excluded** from the main specification — they are themselves insurance variables, so
including them would make prediction easier while saying less about household
characteristics.

## Results

- **Income, education, and household size** are the most stable predictors of coverage size.
- **Regularisation helps, but modestly.** Across 30 repeated train/test splits, Extended
  Ridge has the lowest mean test RMSE, with Lasso close behind.
- The cautious conclusion: richer models improve predictive performance, but a transparent
  OLS model remains necessary for substantive interpretation.

Coefficients are estimated on the full positive-coverage sample with HC3 robust standard
errors. The main split is 75/25; because a single split is noisy at n = 275, evaluation is
repeated over 30 random splits.

## Reproducing

Run the notebook from the repository root so the relative data path resolves:

```bash
pip install pandas numpy matplotlib statsmodels scikit-learn
jupyter lab term_life_analysis.ipynb
```

Seeds: the main train/test split uses `random_state=123`; the repeated-split robustness
check uses seeds 100–129.

## Contents

```
├── term_life_analysis.ipynb   # Data inspection, modelling, robustness, classification extension
├── Term Life Insurance.csv    # 2004 SCF extract (must stay beside the notebook)
├── term_life_q3_report.tex    # LaTeX source for the written report
└── figures/                   # Generated figures
```

---

Originally submitted as assessed coursework for ME315, Department of Statistics, LSE.
