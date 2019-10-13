
`runner` a R package for running operations.
============================================

<img src="vignettes/images/hexlogo.png" align="right" />
========================================================


About
-----

Package contains standard running functions (aka. windowed, rolling, cumulative) with additional options. `runner` provides extended functionality like date windows, handling missings and varying window size. `runner` brings also rolling streak and rollin which, what extends beyond range of functions already implemented in R packages.

Installation
------------

Install package from from github or from CRAN.

``` r
# devtools::install_github("gogonzo/runner")
install.packages("runner")
```

Using runner
------------

`runner` package provides functions applied on running windows. Diagram below illustrates what running windows are - in this case running `k = 4` windows. For each of 15 elements of a vector each window contains current 4 elements (exception are first k - 1 elements where window is not complete).

![](reference/figures/running_windows_explain.png)

Using `runner` one can apply any R function `f` in running window of length defined by `k`, window `lag`, observation indexes `idx`.

![](reference/figures/using_runner.png)

### Window size

`k` denotes number of elements in window. If `k` is a single value then window size is constant for all elements of x. For varying window size one should specify `k` as integer vector of `length(k) == length(x)` where each element of `k` defines window length. If `k` is empty it means that window will be cumulative (like `base::cumsum`). Example below illustrates window of `k = 4` for 10'th element of vector `x`. ![](reference/figures/constant_window.png)

### Window lag

`lag` denotes how many observations windows will be lagged by. If `lag` is a single value than it's constant for all elements of x. For varying lag size one should specify `lag` as integer vector of `length(lag) == length(x)` where each element of `lag` defines lag of window. Default value of `lag = 0`. Example below illustrates window of `k = 4` lagged by `lag = 2` for 10'th element of vector `x`.

![](reference/figures/lagged_window_k_lag.png)

### Windows depending on date

Sometimes data points in dataset are not equally spaced (missing weeekends, holidays, other missings) and thus window size should vary to keep expected time frame. If one specifies `idx` argument, than running functions are applied on windows depending on date. `idx` should be the same length as `x` of class `Date` or `integer`. Including `idx` can be combined with varying window size, than k will denote number of periods in window different for each data point. Example below illustrates window of size `k = 4` lagged by `lag = 2` periods for 10'th element of vector `x`. This (10th) element has `idx = 13` which means that window ranges `[8, 11]` - although `k = 4` only two elements of `x` are within this window.

![](reference/figures/custom_idx_k_lag.png)

### Build-in functions

With `runner` one can use any R functions, but some of them are optimized for speed reasons. These functions are:
- aggregating functions - `length_run`, `min_run`, `max_run`, `minmax_run`, `sum_run`, `mean_run`, `streak_run`
- utility functions - `fill_run`, `lag_run`, `which_run`
