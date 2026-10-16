# econ3916-lab07-bootstrapping
econ3916-lab07-bootstrapping
# Estimation & Bootstrapping — Quantifying Uncertainty Without a Formula

## Objective

I wanted to measure how uncertain an estimate is, first with the CLT formula and then with the bootstrap, and to see where each method works and where it does not.

## Methodology

- Loaded the UCI Adult Census Income data (32,561 respondents).
- Separated the standard deviation of the data from the standard error of an estimate, and checked the s/sqrt(n) relationship across four sample sizes.
- Built parametric confidence intervals from the CLT for age and for capital gains.
- Ran the bootstrap by hand, then with scipy.stats.bootstrap.
- Compared percentile and BCa intervals on a heavily skewed variable.
- Bootstrapped a two-sample difference in mean weekly hours.
- Asked an AI to write a bootstrap-interval function, revised my prompt once, and checked the function against my own intervals.
- Ran a coverage simulation on lognormal data at n=50, for both the mean and the median.

## Key Findings

- The standard deviation describes how spread out people are, and it does not change with sample size. The standard error describes how precise the estimate is, and it shrinks as the sample grows.
- The CLT converges quickly for age and slowly for capital gains, so I trusted the parametric interval sooner for age than for capital gains.
- The bootstrap standard error of the median of 32,561 whole-number ages is exactly 0.0000. With that many ties, every resample returns the same median, so the median is pinned. The bootstrap is reporting a real property of the data, not failing.
- Percentile and BCa intervals can differ on a heavily skewed variable.
- For the mean, the nominal 95% parametric interval covered 92.5% and the percentile bootstrap covered 91.5%. That gap is inside the Monte Carlo standard error of about 1.3 points, so the two methods are indistinguishable here, and both under-cover slightly.
- For the median, the mean-centred parametric interval covered only about 66.8%, while the bootstrap held near its nominal level. When no formula exists for the statistic, the bootstrap is the better tool.
- The AI-written function was only as good as my prompt. It guessed about reproducibility until I specified a seed, and checking it against my own intervals showed me the method was right.
