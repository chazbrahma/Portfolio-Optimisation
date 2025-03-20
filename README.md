# Portfolio-Optimisation

# Introduction
This repository demonstrates a quantitative approach to Modern Portfolio Theory (MPT) using publicly available market data. The goal is to find an optimal portfolio allocation that maximizes the risk-adjusted return (Sharpe Ratio) while respecting practical constraints, such as a minimum weight per asset.

In simpler terms, we are trying to answer questions like:

Which combination of stocks yields the highest return for a given level of risk?
How do we visualize the trade-off between risk and return (the efficient frontier)?
How can we ensure that each asset gets a certain minimum share in the portfolio (so we don’t end up with zero allocation in assets we find valuable)?
How do we deploy actual capital using these final weights (e.g., how many shares to buy with a fixed investment)?
By blending classical MPT with practical constraints, we produce a more “real-world” solution, suitable for a portfolio manager or a quant researcher’s daily workflow.

# Data & Tickers
Tickers Used: AAPL, MSFT, GOOGL, AMZN, TSLA
Data Source: Downloaded from Yahoo Finance
Date Range: 2020-01-01 to 2025-01-01
Price Type: “Close” or “Adj Close,” depending on preferences. For unadjusted data, “Close” is used with auto_adjust=False.
During the data collection step:

We fetched daily closing prices for each ticker.
We computed daily returns as the percentage change from one day’s close to the next.
We annualized the average daily returns and the covariance matrix by multiplying by 252 (typical number of trading days per year).

# Key Steps
1. Portfolio Performance Calculation
Each portfolio is defined by a set of weights that sum to 1 (or 100%). We calculate:

Portfolio Return: The sum of (weight × annual return) across all assets.
Portfolio Volatility: The square root of (weights × covariance matrix × weightsᵀ).
Sharpe Ratio: (Portfolio Return − Risk-Free Rate) / Portfolio Volatility.
2. Maximum Sharpe Optimization
Using numerical optimization (e.g., SLSQP), we minimize the negative Sharpe ratio. This effectively maximizes the Sharpe ratio to find the portfolio with the best risk-return trade-off.

Without Bounds: The solver might push certain weights to zero.
Minimum Weight Bounds: For more practical allocations, we can enforce a lower bound (e.g., 5%) per asset. This ensures no ticker is completely excluded.
3. Efficient Frontier
We also compute the efficient frontier by targeting different levels of annual return and minimizing volatility. Each point on this frontier is an “efficient” portfolio—there is no better solution that offers a higher return at the same risk or lower risk at the same return.

4. Random Portfolios
To give a sense of scale, we generate random portfolios by assigning random weights (that sum to 1) and plot them. This cluster of points often scatters below (or around) the efficient frontier, highlighting how random guesses rarely match a well-optimized result.

5. Capital Deployment
To see how the final solution translates into practical trades, we assume a certain investment amount (e.g., $100,000).

Allocate that total capital by each ticker’s weight.
Divide by the latest price to figure out how many shares to buy.
Floor to an integer so you can’t buy partial shares.
Summarize how much capital was actually spent on each ticker and note any leftover cash.

# Figures
Two main figures appear in this repository:

# Efficient Frontier (Min Weight)

Shows the risk–return “frontier” as a dashed line.
Depicts random portfolios as scattered light-blue dots.
Highlights the “Max Sharpe” portfolio with a large red star.

# Portfolio Allocation (Pie Chart)

Reveals the final distribution of weights across the tickers, after optimization.
For example, a solution might assign ~35% to AAPL, ~43% to TSLA, ~5% each to MSFT and AMZN, and ~11% to GOOGL.
This result depends on your chosen bounds (e.g., 5% min weight) and data.

# Sample Results & Analysis
Below is an illustrative example of the final output you might see:

Optimal Weights (with min weight = 5%)

AAPL: ~35%
MSFT: ~5%
GOOGL: ~11%
AMZN: ~5%
TSLA: ~44%
Performance Metrics

Annual Return: ~49%
Volatility: ~40%
Sharpe Ratio: ~1.16
Capital Deployment ($100,000 example)

AAPL: ~$35,000
MSFT: ~$5,000
GOOGL: ~$11,000
AMZN: ~$5,000
TSLA: ~$44,000
Leftover Cash: ~$1,000

# Interpretation:

The solver suggests large allocations to assets with high returns, but also decent risk–adjusted potential.
The minimum weight constraint ensures at least 5% in MSFT and AMZN, preventing them from dropping to 0%.
Depending on market conditions, these numbers might shift drastically (e.g., if TSLA had extremely high variance, the solver might exclude it if not forced by min weights).


# Why We Might See “Strange” Allocations
Zero Weights: Without minimum weight bounds, some tickers might get 0%. If the solver believes an asset isn’t improving the risk-return trade-off, it excludes it.
High Concentrations: If a particular asset offers unusually high returns relative to its risk, the model might heavily overweight it. This is mathematically correct under MPT assumptions but might be undesirable in real life (leading to poor diversification).
Solver Warnings: If SciPy warns about “values in x being outside bounds,” it means the iterative process tested a solution outside your [min, max] constraints. It clamps them back in range and continues.

# Conclusion
This Portfolio Optimization pipeline demonstrates how to:

Download & Clean stock data,
Compute returns and risk metrics,
Solve for a maximum Sharpe ratio portfolio under constraints,
Visualize the result with an efficient frontier and a final portfolio allocation chart,
Deploy capital in a real-world sense by calculating share counts and leftover cash.
By incorporating practical constraints (like a minimum weight) and capital-based share calculations, this approach moves closer to real-world usage compared to a purely theoretical MPT model. The final results provide a strong foundation for further enhancements, such as:

Extending to more tickers and different asset classes (bonds, commodities).
Introducing transaction costs and short-selling constraints.
Using advanced risk measures (e.g., CVaR) instead of standard deviation.
Periodically rebalancing to maintain target weights.
Whether you’re a quant researcher, portfolio manager, or finance student, these concepts and visual outputs offer deep insights into how your portfolio balances risk vs. return — and how you can tune constraints to align with your personal or institutional risk preferences.

# Future Work
Include Additional Asset Classes

Integrate bonds, commodities, and cryptocurrencies for a more diversified portfolio.
Investigate how correlations change when mixing traditional and alternative assets.
Advanced Risk Measures

Replace standard deviation with Conditional Value at Risk (CVaR) or Drawdown-based metrics.
Incorporate tail-risk management or downside risk approaches for more robust optimization.
Transaction Costs and Slippage

Model bid-ask spreads, commissions, and market impact.
Re-run optimizations to see if small trades or frequent rebalancing are cost-effective.
Dynamic or Rolling Optimization

Use rolling windows of historical data (e.g., last 1-year) to update portfolio weights periodically.
Investigate how shifting market conditions affect the “optimal” solution over time.
Robust / Bayesian Approaches

Account for estimation errors in returns and covariances with robust or Bayesian optimization.
Stress-test the portfolio for different macroeconomic scenarios.
Deployment

Wrap the final code into a web dashboard (e.g., Streamlit) for real-time usage.
Automate data fetching and rebalancing triggers to handle daily or weekly updates.

# Acknowledgments
Author: This project is courtesy of Chazin Brahma, who assembled a clear, quant-focused pipeline blending Modern Portfolio Theory with real-world constraints.
Libraries:
pandas, numpy, matplotlib, seaborn for data manipulation and visualization,
yfinance for fetching historical price data,
scipy for numerical optimization.
Inspiration: Classic portfolio theory from Markowitz, combined with practical touches (capital deployment, minimum weights) that appeal to real quant usage.





