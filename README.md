# Trader Performance vs Bitcoin Market Sentiment

## Objective
Analyze how Hyperliquid trader behavior and performance vary across Bitcoin Fear & Greed regimes, identify behavioral patterns, and derive strategy-relevant insights.

## Data
- Historical trader data: 211,224 trade rows, 16 original columns.
- Fear & Greed Index: daily sentiment score and classification.
- Join key: calendar date derived from `Timestamp IST` and the sentiment dataset date.

## Method
1. Parse and validate dates.
2. Left-join daily sentiment onto each trade.
3. Create net PnL = Closed PnL - Fee.
4. Separate all executions from closing trades (`Closed PnL != 0`) for win-rate analysis.
5. Aggregate performance by sentiment, side, date, and account.
6. Test monotonic association using Spearman correlation at daily-account level.
7. Inspect account concentration and side asymmetry.

## Main Findings
- Fear generated the highest aggregate net PnL in this sample.
- Extreme Greed had the highest closing-trade win rate.
- SELL executions were especially profitable during Extreme Greed, suggesting strong payoff asymmetry in euphoric conditions.
- Sentiment score had only a weak positive Spearman relationship with daily-account PnL (~0.066), so sentiment alone is not a strong standalone predictor.
- Trading activity and volume were slightly lower as sentiment score increased, while PnL had a stronger relationship with activity and volume than with sentiment itself.
- Performance is highly concentrated among a small number of accounts, so aggregate regime results should not be treated as representative of every trader.

## Strategy Implications
- Use sentiment as a regime filter, not a standalone entry signal.
- In Extreme Greed, investigate short/SELL setups with strict risk controls.
- In Fear, opportunity exists but position sizing and trader selection matter because aggregate profitability can be driven by a subset of accounts.
- Evaluate strategies per account and out-of-sample before deployment.
- Include fees in all strategy evaluation because many zero-gross-PnL executions become negative after costs.

## Reproducibility
Open `analysis.ipynb` and run all cells after placing the two CSV files in the expected input paths, or adjust the path variables in the first code cell.

## Deliverables
- `analysis.ipynb`
- `final_report.pdf`
- `outputs/sentiment_performance_summary.csv`
- `outputs/side_sentiment_summary.csv`
- `outputs/account_performance.csv`
- `outputs/spearman_correlations.csv`
- charts in `outputs/`
