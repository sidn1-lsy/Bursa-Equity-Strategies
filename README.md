# Bursa Equity Strategies

A collection of three standalone Python/Jupyter workflows for screening and sizing **29 Bursa Malaysia (`.KL`) stocks** using `yfinance`. Each notebook serves a different purpose and can be run independently using the shared `malaysia_stocks.csv` universe.

## Shared Input File
- `malaysia_stocks.csv`: List of 29 Malaysian equities (company names and `.KL` tickers) used across all three notebooks.

---

## Notebooks Overview

### 1. `01_equal_weights.ipynb` — Equal-Weight Top-10 Market Cap Sizing
- **Purpose:** Ranks the 29 stocks by market capitalization, selects the top 10, divides a user-entered investment amount equally across them, and calculates how many shares to buy per stock.
- **How it works:** Fetches latest closing prices and market caps via `yfinance`, sorts descending by market cap, takes the top 10 companies, prompts for a total portfolio size, splits capital evenly (`portfolio_size / 10`), and floors `position_size / price` to get share quantities.

### 2. `02_value_investing.ipynb` — Valuation Ratio Ranking
- **Purpose:** Evaluates and ranks all 29 stocks across valuation multiples to compute a composite `Value Score`.
- **How it works:** Pulls `PE-Ratio` (`forwardPE`), `PB-Ratio`, `PS-Ratio`, `EV/EBITDA`, and `EV/GP` via `yfinance`, fills missing values with column means, converts each metric into a percentile score (`0` to `1`), averages the percentiles into a `Value Score`, and sorts the table descending.

### 3. `03_dividend_based_investing.ipynb` — Weighted Dividend Scoring
- **Purpose:** Scores and ranks the 29 stocks based on dividend income and earnings growth metrics.
- **How it works:** Retrieves `Dividend Yield(%)`, `Dividend Rate`, `Payout Ratio(%)`, `5 Year Avg Dividend Yield(%)`, and `Earning Growth(%)` via `yfinance`, normalizes each metric between `0` and `1`, applies weights (`0.30`, `0.20`, `0.20`, `0.20`, `0.10`), and ranks stocks by the resulting `Dividend Score`.

---

## Notes & Limitations
- Data is pulled dynamically via `yfinance`, so prices, fundamentals, and rankings reflect live/current snapshots rather than a historical backtest.
- Missing fundamental fields (such as `EV/EBITDA` or `EV/GP` for financial/bank tickers, or occasional `NaN` values in dividend/growth fields) affect normalized/percentile scores.
