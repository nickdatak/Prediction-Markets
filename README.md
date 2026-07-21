# Prediction Markets — Solar Hedge Worked Example

This repository estimates TAN's election-probability exposure, validates the frozen estimate out of sample, costs a prediction-market hedge, and snapshots a screened Kalshi contract universe.

## Execution order

1. `00_data.ipynb` — pull TAN/SPY daily data and Polymarket Trump-Yes prices; build the merged daily dataset.
2. `01_estimate_delta.ipynb` — estimate the baseline and high-signal event-window specifications; produce the frozen headline estimate.
3. `02_validation.ipynb` — freeze the estimate at the November 4, 2024 20:00 UTC equity close and evaluate its realized deviation.
4. `03_hedge.ipynb` — construct and cost retail and institutional hedge scenarios.
5. `04_pnl.ipynb` — calculate four P&L paths and decompose the five-day hedged residual.
6. `05_kalshi_census.ipynb` — download and screen the active standalone Kalshi contract universe.

Run the notebooks in this order. The public APIs are live, so rerunning the Polymarket/Kalshi pulls can change snapshot results.

## Frozen headline numbers

All election-horizon calculations use the November 4, 2024 20:00 UTC entry timestamp.

- Phase 1 high-signal headline estimate: ΔE = **−0.234202**; Newey–West SE(5) = **0.112716**; N = **15**.
- Entry midpoint probability: **0.5785**.
- Phase 2 predicted TAN market-adjusted move: **−9.87%**.
- One-day ΔE estimation error: **32.19%** (−3.18 percentage points of Q).
- Five-day total realized deviation: **104.99%**, primarily reflecting the **−7.19 pp** equity-lag/convergence component.

## Kalshi census snapshot

This frozen census uses a market-list snapshot at **2026-07-21 14:46:31 UTC**, followed by a live order-book collection window from **14:47:03 to 14:47:35 UTC**. It contains 69,716 active standalone contracts before research filtering and 28,022 after filtering to macro, policy, single-industry, and geopolitical categories.

The complete raw census is stored as `data/kalshi_active_contracts_full.csv.gz` to keep repository size manageable. The smaller screened research universe remains available at `data/kalshi_active_contracts_filtered.csv`. The live multi-level $10,000 / 5¢ screen retains **360 contracts** based on cumulative YES-ask capacity, not just best-level depth. The liquid CSV and metadata JSON carry the exact order-book collection window.
