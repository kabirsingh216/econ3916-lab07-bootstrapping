# Estimation & Bootstrapping — Quantifying Uncertainty Without a Formula

## Objective
I wanted to measure how uncertain an estimate is, first with formulas based on the CLT and then with the bootstrap, and to see where each approach works and where it doesn't.

## Methodology
- Loaded the UCI Adult Census Income data (32,561 respondents).
- Separated the standard deviation of the data from the standard error of an estimate, and checked the s/sqrt(n) relationship across four sample sizes.
- Built parametric confidence intervals from the CLT for age and for capital gains.
- Ran the bootstrap by hand, then with `scipy.stats.bootstrap`.
- Compared percentile and BCa intervals on a heavily skewed variable.
- Bootstrapped a two-sample difference in mean weekly hours.
- Asked an AI to write a bootstrap-interval function, revised my prompt once, and checked the function against my own intervals.
- Ran a coverage simulation on lognormal data at n=50, comparing the nominal 95% parametric interval with the percentile bootstrap interval for both the mean and the median.

## Key Findings
- The CLT converges quickly for age and slowly for capital gains.
- The bootstrap SE of the median of the 32,561 whole-number ages is exactly 0.0000. With that many ties, every resample returns the same median. The bootstrap is reporting a real property of the data, not failing.
- For the mean, at n=50 on lognormal data, the parametric interval covered 92.5% and the percentile bootstrap covered 91.5%. The gap is inside the Monte Carlo standard error of about 1.3 points, so I can't tell the two methods apart here. Both under-cover slightly.
- For the median, the mean-centred parametric interval covered only about 66.8%, while the bootstrap held near its nominal level.
