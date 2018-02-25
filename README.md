<!-- README.md is generated from README.Rmd. Please edit that file -->
Sparse Gaussian Markov Random Field Mixtures for Anomaly Detection
==================================================================

#### *Koji Makiyama (@hoxo\_m)*

1 Overview
----------

The **sGMRFmix** package provides an implementation of the algorithm
presented by Ide et al. (2016). It is a novel anomaly detection method
for multivariate noisy sensor data. It can automatically handle multiple
operational modes. And it can also compute variable-wise anomaly scores.

First, we ready a multivariate training data that contains no anomaly
observations. It consists of four parts and repeats two operational
modes.

``` r
library(sGMRFmix)
set.seed(314)
train_data <- generate_train_data()
plot_multivariate_data(train_data)
```

![](README-images/unnamed-chunk-2-1.png)

Second, we ready a multivariate test data that contains some anomaly
values. It consists of 500 normal observations and 500 anomaly
observations. The normal part in the test data consists of two
operational modes that also have seen in the training data. Note that
the variable `x5` has no difference in the normal and anomaly part.

``` r
test_data <- generate_test_data()
plot_multivariate_data(test_data)
```

![](README-images/unnamed-chunk-3-1.png)

We input the training data to the `sGMRFmix()` function to learn the two
operational modes. Then we compute variable-wise anomaly scores for test
data using the result.

``` r
fit <- sGMRFmix(train_data, K = 7, rho = 1.1, verbose = FALSE)
anomaly_score <- compute_anomaly_score(fit, test_data)
plot_multivariate_data(anomaly_score) + ylim(0, 30)
```

![](README-images/unnamed-chunk-4-1.png)

You can see that anomalies are found in the latter part of the test
data. And you can also see the variable `x5` has no high anomaly scores.

2 Installation
--------------

You can install the package from GitHub.

``` r
install.packages("devtools") # if you have not installed "devtools" package
devtools::install_github("hoxo-m/sGMRFmix")
```

The source code for **sGMRFmix** package is available on GitHub at

<https://github.com/hoxo-m/sGMRFmix>.

3 Details
---------

4 Related Work
--------------

5 References
------------

-   \[1\] T. Ide, A .Khandelwal, J .Kalagnanam, **Sparse Gaussian Markov
    Random Field Mixtures for Anomaly Detection**, IEEE 16th
    International Conference on Data Mining (ICDM), 2016, pp 955–960
