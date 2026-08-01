# Portfolio Value at Risk (VaR) Model

Estimates 1-day 95% VaR for a 15-stock portfolio using three methods:
historical simulation, parametric (variance-covariance), and Monte Carlo
simulation. Backtested using a rolling 252-day window over a ~5-year
sample (1,002 out-of-sample observations).

## Results

**95% 1-Day VaR estimates (full sample, $1,000,000 portfolio):**

| Method | VaR (%) | VaR ($) |
|---|---|---|
| Historical | 1.86% | $18,626 |
| Parametric | 1.84% | $18,364 |
| Monte Carlo | 1.84% | $18,386 |

**Backtest violation rates** (target: ~5%, 1,002 trading days tested):

| Method | Violation rate |
|---|---|
| Historical | 5.59% |
| Parametric | 5.89% |
| Monte Carlo | 5.79% |

## Key findings

All three methods converge tightly (within 2 basis points of each other),
suggesting the portfolio's return distribution over this sample period
doesn't exhibit strongly fat tails relative to a normal distribution —
the divergence between historical and parametric VaR that's often
expected in practice is minimal here.

All three violation rates land slightly above the 5% target (5.6–5.9%),
consistently across methods. This is close enough to be a reasonably
well-calibrated model, but the consistent direction (all three
overshooting, none undershooting) is worth flagging rather than
dismissing as noise — it could suggest the 252-day lookback window
reacts slightly too slowly to rising volatility, causing marginally
more breaches than the target rate.

## Limitations

- Parametric and Monte Carlo methods both assume normally distributed
  returns; Monte Carlo's realism comes from capturing cross-asset
  correlation, not from relaxing the normality assumption itself.
- Equal-weighted portfolio (1/15 per stock) — not reflective of a
  real, conviction-weighted or market-cap-weighted portfolio.
- 252-day lookback window is a standard convention, not a tuned
  parameter — a shorter window might reduce the slight overshoot in
  violation rates at the cost of more noise.

## Tools

Python, pandas, numpy, scipy, yfinance, matplotlib — built in Google Colab.

## Notebook

[View the VAR model notebook](https://github.com/raymonxian-collab/VAR_model.-/blob/main/VAR_MODEL.ipynb)
