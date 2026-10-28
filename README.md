# market-risk-daily-report
# Daily Market Risk Report (Python)

A step-by-step personal learning project: building a daily market risk report
for a small derivatives portfolio, from Black-Scholes Greeks to PnL explain.

## Goal
Explain the daily PnL of an option portfolio using Greeks, and measure how
far the Greeks-based estimate is from full revaluation.

## Contents
- `01_pnl_explain.ipynb`
  - **Part I** – Single long call: price, Greeks, Explained vs Actual PnL, 5 scenarios
  - **Part II** – Portfolio (stock, long call, long put, short call):
    position-level and portfolio Greeks, PnL explain, scenario analysis

## Method
- Explained PnL = Delta + Gamma + Vega + Theta + Rho PnL (portfolio Greeks)
- Actual PnL = full revaluation of every position under the new market state
- Unexplained PnL = Actual - Explained

## Key results
| Scenario | Spot | Explained PnL | Actual PnL | Unexplained PnL | Unexplained / Actual |
|---|---|---|---|---|---|
| Base case (time only) | 100 | -4.96 | -4.99 | -0.03 | 0.7% |
| Spot +2%, Vol +1pt | 102 | 276.30 | 271.70 | -4.60 | 1.7% |
| Spot -2% | 98 | -236.39 | -235.69 | 0.70 | 0.3% |
| Spot +10% (stress up) | 110 | 1,681.97 | 1,478.91 | -203.06 | 13.7% |
| Spot -10% (stress down) | 90 | -808.89 | -715.73 | 93.17 | 13.0% |


- Small moves (+/-2%): Unexplained stays below 2% of Actual PnL.
- Large moves (+/-10%): Unexplained rises to about 13% of Actual PnL, because Gamma
  is treated as constant while it actually changes with spot.
- In both stress cases the Greeks overstate the result (Explained is larger than Actual in absolute value).
- Conclusion: for stress and tail risk, use full revaluation.

## How to run
Python 3, `numpy`, `scipy`, `pandas`, Jupyter.
Open the notebook, then Restart & Run All.

## Roadmap
VaR / Expected Shortfall -> backtesting -> limits & commentary -> bonds (DV01) -> FX & stress testing

## Assumptions
Black-Scholes, European options, no dividends, 365-day calendar.

*Educational project*