# Person 1 — Financial Inclusion EDA: Findings & Interpretation

**Dataset:** World Bank Global Findex, Indonesia 2024 (`IDN_2024_FINDEX_v02_M`)  
**Analysis owner:** Person 1 (`rrrafaa`)  
**Notebook:** [04 — Financial Inclusion EDA](../notebooks/04_eda_inclusion.ipynb)  
**Status:** **Preliminary descriptive EDA**. Notebook 02 variable mapping and Notebook 03 shared cleaning must be reviewed before dashboard finalization.

## Executive summary

Account ownership is estimated at **56.33%** using the survey weight `wgt`. Of the five tested dimensions (income quintile, education, age group, gender and urban/rural residence), the biggest *descriptive* difference in account ownership is by **education (47.97 percentage points)**, followed by the maximum-minus-minimum **income-quintile gap (31.80 pp, Q5 vs Q3)** and **age-group gap (30.62 pp, age 25–34 vs 55+)**. Using the more interpretable highest-versus-lowest **income Q5–Q1** comparison yields **31.58 pp**. Gender and urban/rural differences are substantially smaller.

These are weighted descriptive estimates, not causal relationships or statistical significance tests.

## 1. Overview: national indicators

| Indicator | Weighted rate |
|---|---:|
| Owns an account (`account`) | **56.33%** |
| Financial institution account (`account_fin`) | 52.39% |
| Mobile money account (`account_mob`) | 22.01% |
| Digital payment (`anydigpayment`) | 42.69% |
| Saved money (`saved`) | 52.99% |
| Borrowed money (`borrowed`) | 47.64% |

**Interpretation:** More than half the represented adult population owns an account, but substantial nonownership remains. Digital-payment use is lower than account ownership. These indicators can overlap and use distinct measurement definitions; do **not** interpret differences as a conversion funnel or sum the percentages.

## 2. Income gap

| Income quintile | Owns an account |
|---|---:|
| Q1 (lowest income) | 46.425% |
| Q2 | 50.406% |
| Q3 | 46.203% |
| Q4 | 60.590% |
| Q5 (highest income) | 78.002% |

**Q5–Q1:** 31.577 pp (rounded to 31.58 pp). **Highest–lowest observed group:** Q5–Q3 = 31.799 pp (rounded to 31.80 pp). The pattern is **not strictly monotonic**, since Q3 is slightly below Q1. This makes group comparison and interpretation more accurate than saying every higher income quintile has greater ownership.

## 3. Education gap — highest descriptive disparity

| Education | Rate | Unweighted sample n |
|---|---:|---:|
| Primary or less | 37.638% | 380 |
| Secondary | 66.268% | 646 |
| Tertiary or higher | 85.607% | 41 |

**Tertiary vs primary:** **47.969 pp (47.97 pp)**. Caution: the tertiary group has only **41** unweighted respondents. One respondent lacks an education code; the missing category is **excluded from substantive comparisons and public visualizations**. A revised grouping rule is already in the notebook; rerun the subgroup chart cell after opening the updated GitHub version.

## 4. Age gap

| Age group | Rate |
|---|---:|
| 15–24 | 61.993% |
| 25–34 | 70.135% |
| 35–44 | 61.054% |
| 45–54 | 45.226% |
| 55+ | 39.519% |

The **25–34 vs 55+** difference is **30.616 pp (30.62 pp)**. This is a descriptive association, not evidence that age causes financial exclusion.

## 5. Gender and residence

| Group | Account ownership |
|---|---:|
| Female | 58.031% |
| Male | 54.639% |
| Urban | 56.666% |
| Rural | 56.030% |

Gender difference: **3.392 pp (3.39 pp)**. Urban–rural difference: **0.636 pp (0.64 pp)**. These small differences are not established as statistically significant.

For a separate example where the pattern differs by outcome, mobile money account ownership is **24.131% for men** versus **19.878% for women**; rates should be compared indicator by indicator rather than claiming one gender consistently leads.

## 6. Business implications to investigate

- **Financial accessibility / affordability:** Explore why lower-income quintiles have notably lower account ownership; avoid attributing it to fees or lack of income without directly testing those survey questions.
- **Education and financial literacy:** Investigate whether product literacy and onboarding usability may matter. Education categories do not directly measure financial literacy.
- **Age-inclusive service design:** Explore assisted onboarding and simpler user experience for older groups; this is a hypothesis, not an experimentally verified intervention.
- **Inclusive digital finance:** Evaluate account ownership, mobile money and payments together while preserving each indicator's distinct definition.

## 7. Methodological limits

- Based on a **single-year, cross-sectional** national survey (2024); no trends or causality are identified.
- Weighted proportions use `SUM(wgt × binary_indicator) / SUM(wgt)` among valid responses; group gaps are **percentage-point** differences.
- No confidence intervals, complex-survey variance estimates or statistical significance tests are included.
- The simple `n < 30` warning is not a substitute for uncertainty estimation. Caution also applies to n=41 in the tertiary category.
- There is **no provincial variable** in this input; do not create province rankings or province choropleths from it.
- The original run included a missing-education `n=1` display, removed from the public notebook along with respondent previews. The cleaned chart needs to be rerun.
- Survey question definitions, survey eligibility and categorical mappings must be cross-checked with [the official World Bank codebook](https://microdata.worldbank.org/catalog/7917/data-dictionary/F1) during Notebook 02/03 review.

## 8. Next steps and roles

| Order | Owner | Deliverable |
|---|---|---|
| 1 | Person 1 | Rerun Notebook 04 from the updated GitHub source so the revised subgroup chart excludes missing education; inspect new graphs |
| 2 | Person 2 | Finish Notebook 02 (definitions, eligible responses, missing/skip logic) |
| 3 | Both | Finish Notebook 03; agree on canonical mappings, cleaning and weighted formulas |
| 4 | Person 1 | Recompute Notebook 04 with the agreed transformation and validate the national KPI |
| 5 | Both | Cross-review and approve aggregated tables for Google Sheets / Looker Studio; keep raw respondent data private |
| 6 | Person 1 | Build Dashboard Page 1 (Overview) and Page 2 (Inclusion & Demographic Gap) |
| 7 | Person 2 | Build Page 3 (Digital Finance) and Page 4 (Financial Barriers) |
| 8 | Both | Test filters and metric consistency; add dashboard link, screenshots, methodology and final narrative to README |

**Suggested dashboard headline:** *Income, education, and age show considerably larger descriptive differences in account ownership than gender or rural/urban residence in Indonesia’s 2024 Findex survey.*
