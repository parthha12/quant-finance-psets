# Time series & correlation

Source: [`time_series_assignment.pdf`](time_series_assignment.pdf)

## Question 1

Why identical correlation coefficients do not imply the same relationship: Pearson's correlation coefficient \(r\) measures only the strength and direction of a **linear** relationship between two variables.

- **Pair A:** reflects a true, consistent linear dependence.
- **Pair B:** has a non-linear (curved) relationship where Pearson correlation fails to capture the true underlying structure. Pearson's \(r\) is also extremely sensitive to outliers; a single extreme observation can artificially inflate or deflate the correlation coefficient, similar to Anscombe's Quartet.

What an analyst should examine:

- **Scatter plots:** visually inspect the data for non-linearity, heteroscedasticity, or clustering.
- **Outliers and leverage points:** identify extreme values that disproportionately influence the summary statistic.
- **Alternative metrics:** use rank-based non-parametric correlations such as Spearman's rank or Kendall's tau if appropriate.

## Question 2

What high lag-1 autocorrelation actually tells us: high lag-1 autocorrelation in closing prices indicates strong persistence or inertia in price levels, meaning today's price is very close to yesterday's price.

Why it does not imply predictable or profitable returns:

- **Prices vs. returns:** high autocorrelation in prices is a standard feature of non-stationary series such as a random walk.

\[
S_t = S_{t-1} + \varepsilon_t
\]

Trading profitability depends on predicting returns, not price levels:

\[
R_t = \frac{S_t - S_{t-1}}{S_{t-1}}
\]

In a random walk, price levels can be highly autocorrelated while price changes are unpredictable white noise.

- **Transaction costs and spreads:** even if a small predictable component exists in returns, bid-ask spreads and execution costs can eliminate the theoretical profit margin.

## Question 3

Why this is a problem: an upward trend implies non-stationarity; specifically, the mean of the series changes over time. Models trained on non-stationary data can break down out of sample because statistical properties are not stable across time.

Transformations to achieve stationarity:

- **Differencing:** take first differences.

\[
\Delta S_t = S_t - S_{t-1}
\]

- **Log returns:** calculate changes in log prices, which remove the price-level trend and are often more suitable for modeling.

\[
r_t = \ln(S_t) - \ln(S_{t-1})
\]

## Question 4

Diagnostic advantage of keeping provider datasets separate: keeping Bloomberg and FactSet data separate creates a clean framework for cross-provider benchmarking and validation.

What differences help you learn:

- **Data handling and adjustments:** discrepancies can reveal different treatments of stock splits, dividends, spinoffs, and other corporate actions.
- **Survivorship and restatement bias:** differences can reveal how providers handle delisted firms, historical revisions, or point-in-time filing dates.
- **Strategy sensitivity:** comparison helps determine whether a quantitative signal is robust or overly sensitive to vendor-specific formatting and timing definitions.

## Question 5

Proof:

1. Express \(X_t - X_{t-1}\) using the log definition:

\[
X_t - X_{t-1} = \ln(S_t / S_0) - \ln(S_{t-1} / S_0)
\]

2. Apply the logarithm quotient rule:

\[
X_t - X_{t-1} = \ln\left[\frac{S_t / S_0}{S_{t-1} / S_0}\right] = \ln(S_t / S_{t-1})
\]

3. Express \(S_t / S_{t-1}\) in terms of nominal return \(R_t\):

\[
1 + R_t = 1 + (S_t / S_{t-1} - 1) = S_t / S_{t-1}
\]

4. Substitute back:

\[
X_t - X_{t-1} = \ln(1 + R_t)
\]

Explanation of the approximation: using the Taylor series expansion of \(\ln(1+r)\) around \(r=0\):

\[
\ln(1+r) = r - \frac{r^2}{2} + \frac{r^3}{3} - \cdots
\]

When \(|r|\) is small, as with many daily asset returns, the higher-order terms become negligible. Therefore:

\[
\ln(1 + R_t) \approx R_t
\]

which yields:

\[
R_t \approx X_t - X_{t-1}
\]
