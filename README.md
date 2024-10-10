# Portfolio-Optimisation

This project aims to optimize portfolio performance by applying portfolio theory and Monte Carlo simulations. It assesses different portfolio strategies under varying market conditions (Bull, Bear, and Sideways) and compares key metrics such as return, risk, and Sharpe ratio for each strategy.

Key Goals of the Project:
Portfolio Optimization: Use historical stock data to create optimized portfolios (Max Sharpe Ratio and Min Risk portfolios) and compare them with an Equal-Weighted portfolio.
Market Condition Analysis: Evaluate portfolio performance under different market conditions (Bull, Bear, Sideways).
Actionable Insights: Provide insights into the best-performing portfolio strategy under different market conditions.

Dataset:
The dataset used for this analysis consists of the adjusted closing prices of several high-performing index funds:

SPY: S&P 500 ETF
VOO: Vanguard S&P 500 ETF
QQQ: Invesco QQQ Trust
IVV: iShares Core S&P 500 ETF
These index funds provide a strong foundation for diversified portfolio strategies.

Key Features:
Adjusted Closing Prices: Used to calculate daily and monthly returns for portfolio analysis.
Portfolio Weights: Randomly generated and optimized weights for different portfolio strategies.
Market Conditions: Classifications of market days into Bull, Bear, and Sideways markets, based on daily stock performance.

Problem Statement:
How can we optimize portfolio performance under different market conditions? This project applies Monte Carlo simulations to evaluate various portfolio strategies, comparing them based on key metrics such as returns, risk, and Sharpe ratios.

Methodology:

Data Preprocessing:
Download Historical Data: Retrieve historical data for index funds using yfinance.
Calculate Returns: Calculate daily returns from adjusted closing prices.
Market Classification: Classify market days into Bull, Bear, and Sideways conditions using a threshold-based approach.

Portfolio Optimization:
Max Sharpe Ratio Portfolio: Optimizes portfolio weights to maximize the Sharpe ratio.
Min Risk Portfolio: Optimizes portfolio weights to minimize risk.
Equal Weighted Portfolio: A portfolio that assigns equal weights to all assets.

Monte Carlo Simulation:
Simulate thousands of random portfolio weights and calculate their returns, risk (volatility), and Sharpe ratios.
Identify the optimal portfolios based on these simulations.

Performance Evaluation by Market Conditions:
Market Condition Classification: Use SPY's daily returns to classify each day into Bull, Bear, or Sideways markets.
Portfolio Returns: Calculate daily returns for Max Sharpe, Min Risk, and Equal-Weighted portfolios.
Performance by Condition: Evaluate portfolio performance metrics (average return, risk, Sharpe ratio) in each market condition.

Visualization and Analysis:
Compare the performance of the three portfolio strategies across different market conditions.
Visualize the results with bar charts and dataframes to better understand performance trends.

Model Evaluation:
Metrics:
Return: The average daily return for each portfolio strategy.
Risk: The standard deviation of returns, representing portfolio volatility.
Sharpe Ratio: A measure of risk-adjusted return.

Results:
After running the Monte Carlo simulation and evaluating portfolio performance, key insights include:
The Max Sharpe Ratio portfolio tends to outperform during Bull markets due to higher returns but exhibits higher volatility.
The Min Risk portfolio performs well in Bear markets, offering more stability with lower volatility.
The Equal Weighted portfolio shows balanced performance across all market conditions, serving as a good default option in uncertain markets.


Future Work:
Exploring Additional Algorithms: Applying different optimization algorithms like Genetic Algorithms or Gradient Descent to enhance portfolio optimization.
Incorporating More Features: Using other economic indicators (e.g., inflation, interest rates) to further refine the model.
Advanced Feature Engineering: Adding features such as asset correlations, which may improve the optimization process.

Visualizations:
Several visualizations were created to analyze portfolio performance under different market conditions:
Bar Plots: Show average returns and risk for each portfolio under Bull, Bear, and Sideways markets.
Efficient Frontier: Displays the trade-off between risk and return for simulated portfolios.

Technologies Used:
Python: The primary language used for data analysis and portfolio optimization.
Jupyter Notebook: Used to develop and run the code interactively.
Pandas & NumPy: For data manipulation and financial calculations.
Matplotlib: For data visualization, particularly portfolio performance under different market conditions.
cvxpy: For solving optimization problems related to portfolio weights.

Conclusion:
This project successfully developed a predictive framework for optimizing portfolios using Monte Carlo simulations and market condition analysis. The results provide valuable insights for investors seeking to adjust their portfolio strategies based on market environments, helping them balance risk and return. Future improvements could include exploring additional optimization algorithms and incorporating more economic data into the model.

