# Variance
#financial analysis#

* How spread out the data is
* In finance, high variance in returns is risky
* Low variance is usually tightly scattered around the mean

```py
# Import libraries
import numpy as np
np.random.seed(121)

# Generate 20 random integers < 100
X = np.random.randint(100, size=20)

# Sort them
X = np.sort(X)
print 'X: %s' %(X)

mu = np.mean(X)
print 'Mean of X:', mu

# X: [ 3  8 34 39 46 52 52 52 54 57 60 65 66 75 83 85 88 94 95 96]
# Mean of X: 60.2
```

**Range**
* `max(data) - min(data)`
* really sensitive since an outlier with little affect on the dataset have severe impact on the range
```py
# ptp means peak to peak
print 'Range of X: %s' %(np.ptp(X))
# Range of X: 96 - 3 = 93
```

**Mean absolute deviation (MAD)**
* `m = \frac{sum_{i=1}^{n} \abs{X_i - \mew}}{n}`
```py
abs_dispersion = [np.abs(mu - x) for x in X]
M = np.sum(abs_dispersion)/len(abs_dispersion)
print 'Mean absolute deviation of X:', M
# Mean absolute deviation of X: 20.52
```

**Variance and standard deviation**
* variance is the average of the squared deviation around the mean
* `variance = \theta^2 = \frac{sum_{i = 1}^{n} (X_i - \mew)^2}{n}`
* `stdev = \sqrt{variance}`
```py
print 'Variance of X:', np.var(X)
print 'Standard deviation of X:', np.std(X)
# Variance of X: 670.16
# Standard deviation of X: 25.8874486962
```
* Notice variance has a different unit of measure (squared) compared to the original data set
* A large variance indicates that numbers in the set are far from the mean and each other, while a small variance indicates the opposite.
* The greater the standard deviation of a security, the greater the variance between each price and the mean, which shows a larger price range. For example, a volatile stock has a high standard deviation, while the deviation of a stable blue-chip stock is usually rather low.
	* A large dispersion shows how much the return on the fund is deviating from the expected normal returns.

**What's the Difference Between Standard Deviation and Mean?**
* Mean is the average of the data points whereas the standard deviation is the measure of how spread apart each point is from the mean. Standard deviation is more useful as a larger number means the returns fluctuate greatly from the mean

**Semivariance and semideviation**
* accounts for only the negative variance from the mean
* eqn is a trivial change from the above formulas
