# Rafa — Data Quality Assessment (Notebook 01)

**Project:** Indonesia Financial Inclusion & Digital Finance Analytics  
**Data source:** World Bank Global Findex, Indonesia survey year 2024  
**Owner:** Rafa (`rrrafaa`)  
**Source of evidence:** [Executed Notebook 01](../notebooks/01_data_profiling.ipynb)  
**Snapshot:** Original successful Google Colab execution (6 / 6 code cells completed, no errors).

## 1. Source validation

| Check | Observation | Assessment |
|---|---:|---|
| Number of respondents | 1,068 | As expected |
| Number of columns | 199 | As expected |
| Survey year | 2024 | As expected |
| Exact file checksum | Matches `data/raw/README.md` | Passed |
| Duplicate full rows | 0 | Passed |
| Duplicate respondent IDs | 0 | Passed |
| Null survey weights | 0 | Passed |
| Non-positive survey weights | 0 | Passed |
| Missing `educ` | 1 | Review during joint cleaning |

Source column types in this CSV: 149 `float64`, 47 `int64`, 3 `object`.

## 2. Survey weights

| Statistic | Value |
|---|---:|
| Count | 1,068 |
| Mean | 1.000 |
| Standard deviation | 0.525 |
| Minimum | 0.258 |
| 25th percentile | 0.616 |
| Median | 0.881 |
| 75th percentile | 1.262 |
| Maximum | 2.818 |
| Kish approximate effective sample size | 837.7 |

**Interpretation:** Final population-like descriptive percentages must be computed using `wgt` over valid responses. Kish effective N is approximate and does not account for the full complex survey design.

## 3. Selected unweighted distributions

These are **raw sample counts**, *not* population-weighted estimates.

| Indicator | Sample counts |
|---|---|
| `female` | 1 = 557; 2 = 511 |
| `educ` | 1 = 380; 2 = 646; 3 = 41; missing = 1 |
| `inc_q` | Q1 = 210; Q2 = 199; Q3 = 210; Q4 = 205; Q5 = 244 |
| `urbanicity` | 1 = 613; 2 = 455 |
| `account` | Yes = 604; No = 464 |
| `account_fin` | Yes = 564; No = 504 |
| `account_mob` | Yes = 209; No = 859 |
| `anydigpayment` | Yes = 444; No = 624 |
| `internet_use` | Yes = 736; No = 332 |

## 4. Missingness and skip logic

- All `fin11a`–`fin11f` have **564 missing rows**. Crosstab verification showed `fin11a` was observed for the 504 nonowners of a financial institution account and missing for the 564 owners.
- This is consistent with **survey skip logic**, not evidence of random data loss. The meanings of individual barrier responses and any nonresponse codes must be cross-checked with the official codebook.
- Several other variables in the profiling table have 100% missingness. Mutia should review their question applicability before dropping columns.
- **Do not replace all missing responses with zero.** Treat not asked, not applicable, refusal, and unknown responses according to the codebook.

## 5. Handoff for EDA Notebook 04

1. Proceed with descriptive exploratory analysis using the original validated file.
2. Compute each indicator as `sum(wgt × indicator) / sum(wgt)` over valid answers, broken down by gender, income, education, residence, and age.
3. Flag subgroups with small unweighted sample sizes; do not interpret gaps as statistically significant without appropriate inference.
4. Once Mutia's codebook mapping and shared cleaning integration are approved, **rerun Notebook 04** using the agreed clean definitions.
5. Publish only aggregates and reviewed non-identifying visualizations; no respondent-level microdata should be committed.

## Repository safety

The raw ZIP and generated `data/processed/*.csv` are excluded from the public repository by `.gitignore`. This document contains only aggregated checks and sample counts.
