# econ5200-lab07-bootstrapping
# Diagnosing Broken Confidence Intervals

## Objective

I investigated why confidence intervals can fail when bootstrap assumptions are violated, data are skewed, or observations are clustered.

## Methodology

- Loaded 32,561 age records and examined the bootstrap distribution of the sample median.
- Calculated the bootstrap standard error and percentile 95% confidence interval, and checked the BCa method for warnings and invalid results.
- Simulated skewed data with a sample size of 50 and conducted 400 experiments to measure the coverage of nominal 95% parametric and bootstrap intervals for the mean and median.
- Compared the i.i.d. bootstrap with the cluster bootstrap using wage data from 25 firms.
- Used a `bootstrap_utils.py` module containing percentile, i.i.d. bootstrap, and cluster bootstrap functions.
- Used AI to write a coverage function, revised my prompt once, and compared its results with my own coverage calculations.

## Key Findings

- **Degenerate bootstrap:** The sample median was 37.0, and the bootstrap standard error was 0.000000. All 2,000 resamples returned the same median, producing a percentile 95% confidence interval of [37.0, 37.0]. The BCa method returned `nan` with a warning instead of an interval.
- **Coverage on skewed data:** For the mean, the parametric interval achieved 92.5% coverage and the bootstrap interval achieved 92.0%. For the median, the parametric interval achieved 66.8% coverage, while the bootstrap interval achieved 92.8%.
- **Clustered wage data:** The naive i.i.d. bootstrap interval was approximately 5.7 times narrower than the cluster bootstrap interval. Across 200 panels, the naive method achieved 19.5% coverage, while resampling whole firms improved coverage to 91.0%.
- **AI-assisted validation:** The AI-written coverage function matched my Diagnosis 3 results exactly. The naive bootstrap coverage was 19.5% for both calculations, and the cluster bootstrap coverage was 91.0% for both, with a difference of 0 percentage points in each case.
