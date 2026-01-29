# Market Simulation Experiments

This repository contains **agent-based market simulation experiments** inspired by Vernon Smith’s classic continuous double-auction studies, in particular the dynamics illustrated in *Smith’s Chart 5*.

The focus of this project is to understand **how automated trading agents behave under structural market changes**, and how closely their price dynamics resemble those observed in human-subject laboratory markets.

---

## Project Motivation

Continuous double-auction markets are often studied through controlled laboratory experiments with human traders. While many automated trading strategies have been proposed, their ability to reproduce key qualitative market dynamics remains an open question.

This project explores whether a heterogeneous population of simple automated traders can:

* converge toward theoretical equilibrium prices,
* respond coherently to sudden structural shocks, and
* exhibit stable post-shock behaviour comparable to experimental results reported in the literature.

Rather than optimising for profit, the emphasis here is on **market-level dynamics and interpretability**.

---

## Market Design

The simulated market follows a Bristol Stock Exchange–style continuous double-auction mechanism with the following structure:

* **Trader population**: equal numbers of ZIP, ZIC, and SHVR agents on both the buy and sell sides
* **Session structure**: six consecutive trading periods, each lasting 300 seconds
* **Supply and demand**:

  * Periods 1–4: static and symmetric schedules
  * Period 5 onward: upward shift in demand while supply remains fixed
* **Equilibrium prices**:

  * Pre-shock equilibrium ≈ 312.5
  * Post-shock equilibrium ≈ 345

Reservation values are reassigned at the start of each period to preserve a clear intra-period structure consistent with Smith’s original experimental design.

---

## Experimental Approach

Because heterogeneous automated agents introduce substantial randomness into transaction sequences, a large number of independent simulations are required to obtain stable qualitative patterns.

* **Number of simulations**: 10,000 independent runs
* **Selection logic**:

  * Period-wise mean transaction prices are computed for each run
  * The representative run is selected by minimising RMSE relative to the theoretical equilibrium path
* **Evaluation focus**:

  * Price convergence under static conditions
  * Adjustment dynamics immediately after the demand shock
  * Price dispersion within and across trading periods

This approach aims to remain faithful to the qualitative reasoning behind Smith’s original analysis while maintaining full reproducibility.

---

## Key Findings

The selected representative run reproduces the main qualitative features of Smith’s Chart 5:

* Prices gradually converge toward equilibrium during the initial static periods
* A clear upward jump follows the introduction of the demand shock
* A brief overshooting phase appears near the end of the shock period
* Prices stabilise around the new equilibrium in subsequent periods

Compared to human-subject laboratory markets, however, intra-period price dispersion remains relatively large. This reflects stochastic trader activation and the presence of random trading strategies within the heterogeneous population.

---

## Interpretation

The results highlight both the strengths and limitations of simple automated trading agents.

Adaptive strategies such as ZIP and SHVR contribute to stabilising prices around equilibrium levels, while random traders introduce persistent noise that prevents the formation of the tight “price tunnel” observed in Smith’s laboratory data.

Overall, the simulation captures the **directional dynamics of equilibrium adjustment**, while illustrating how heterogeneity and stochasticity affect convergence quality in automated markets.

---

## Limitations and Future Work

Several limitations remain.

First, convergence after the demand shock exhibits a noticeable delay relative to human-subject markets. Future work could isolate the effects of trader heterogeneity by varying trader composition and activation rules.

Second, related experiments suggest that strategy performance is highly sensitive to market conditions. Parameter choices that work well in one environment may not generalise across different price scales or volatility regimes.

Finally, preliminary extensions incorporating volatility-aware trading logic indicate potential performance improvements, but broader evaluation across multiple markets, longer horizons, and more diverse trader populations is required before making general claims.

---

## Repository Structure

```
market-simulation-experiments/
├── notebooks/        # Reproducible experiment notebooks
├── src/              # Simulation and evaluation utilities
├── results/
│   ├── figures/      # Transaction price plots and summaries
│   └── tables/       # RMSE and summary statistics
└── notes/            # Experimental assumptions and design notes
```

---

## Author

**Mingyu Wang**
MSc student in Data / FinTech
Bristol, UK

LinkedIn: [https://www.linkedin.com/in/mingyu-wang-555254385](https://www.linkedin.com/in/mingyu-wang-555254385)
