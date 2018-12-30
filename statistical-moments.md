# Statistical Moments - Skewness and kurtosis
#financial analysis#

**Skewness**
* Mean and variance does not give a complete lens into the dataset
* skewness is yet another lens which lets us measure how far to one side of the mean the data biases to
* a normal distribution has a skewness of 0
* skew > 0 has a peak leaning to the left
* skew < 0 has a peak leaning to the right
* S&P 500 returns skewness

```py
start = '2012-01-01'
end = '2015-01-01'
pricing = get_pricing('SPY', fields='price', start_date=start, end_date=end)
returns = pricing.pct_change()[1:]

print 'Skew:', stats.skew(returns)
print 'Mean:', np.mean(returns)
print 'Median:', np.median(returns)

plt.hist(returns, 30);
# Skew: -0.208327061229
# Mean: 0.000732549262327
# Median: 0.000805529770079
```

Negative skewness indicate mean is less than the median

* Skewness is used when judging return distribution
* skewness accounts for extremes rather than honing in on the mean
* Short and medium term investors need to look at the skewness since large sways in returns will not get smoothed out with time
* Skewness is a better prediction on returns compared to standard deviation
	* standard deviation assumes normal distribution which is rarely the case

**Kurtosis**
* measures the shape of deviation
* describes how peaked a distribution is compared to the normal distribution (pointedness)
* Positive -> very pointy
* Negative -> flat

**Jarque Bera**
* statistical test that compares whether the sample has skewness and kurtosis similar to the normal distribution

```py
from statsmodels.stats.stattools import jarque_bera

N = 1000
M = 1000

pvalues = np.ndarray((N))

for i in range(N):
    # Draw M samples from a normal distribution
    X = np.random.normal(0, 1, M);
    _, pvalue, _, _ = jarque_bera(X)
    pvalues[i] = pvalue

# count number of pvalues below our default 0.05 cutoff
num_significant = len(pvalues[pvalues < 0.05])

print float(num_significant) / N
# 0.054
```

* ie, we should expect to be wrong  5%  of the time at a 0.05 significance level

```py
_, pvalue, _, _ = jarque_bera(returns)

if pvalue > 0.05:
    print 'The S&P 500 returns are likely normal.'
else:
    print 'The S&P 500 returns are likely not normal.'
# The S&P 500 returns are likely not normal.
```
