# gbm-stock-simulator

Simulates the evolution of a stock price using a **Geometric Brownian Motion (GBM)** model, via Monte Carlo.

## Context

Built as part of the **Managing Risk** course from EDHEC Business School, on Coursera:
🔗 https://www.coursera.org/learn/portfolio-risk-management-python

## How it works

The model simulates a large number of possible price paths by drawing, at each time step, a random return from a normal distribution with mean `mu*dt` and standard deviation `sigma*√dt`, then compounding these returns to reconstruct the price path.

```python
import numpy as np
import pandas as pd

def gbm(n_years=10, n_scenarios=1000, mu=0.07, sigma=0.15, steps_per_year=12, s_0=100.0):
    """Evolution of a Stock Price using a Geometric Brownian Motion Model"""
    dt = 1/steps_per_year
    n_steps = int(n_years*steps_per_year)
    rets_plus_1 = np.random.normal(loc=(1+mu*dt), scale=(sigma*np.sqrt(dt)), size=(n_steps, n_scenarios))
    prices = s_0*pd.DataFrame(rets_plus_1).cumprod()
    return prices
```

## Parameters

| Parameter | Description | Default |
|---|---|---|
| `n_years` | Simulation horizon (years) | 10 |
| `n_scenarios` | Number of simulated price paths | 1000 |
| `mu` | Expected annualized return (drift) | 0.07 |
| `sigma` | Annualized volatility | 0.15 |
| `steps_per_year` | Granularity (12 = monthly) | 12 |
| `s_0` | Initial price | 100.0 |

## Installation

```bash
pip install numpy pandas matplotlib
```

## Usage

```python
prices = gbm(n_years=10, n_scenarios=500, mu=0.07, sigma=0.15)
prices.plot(legend=False, alpha=0.3, figsize=(12, 6))
```

---

[LinkedIn — Joud Katbe](https://linkedin.com/in/joud-katbe/)
