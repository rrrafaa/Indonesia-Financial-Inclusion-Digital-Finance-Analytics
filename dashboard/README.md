# Looker Studio Dashboard — Findex Indonesia 2024

**Owners:** Rafa (Page 1–2) + Mutia (Page 3–4).  
**Status 19 November 2026:** Notebook 03 QA **14/14 PASS**, Notebook 04 **140/140 KPI PASS**, Notebook 05 **100 digital + 6 barrier + 11 overall PASS**, Notebook 06 **12/12 export QA PASS** (verified from executed Colab). Notebook 06 exports are ready in private Drive. **Looker Studio is not yet built/published.**

[Open executed Notebook 06](https://colab.research.google.com/drive/1b8Qq-upwolz-TnoWRhXluVJvbQ7oyMSc?usp=sharing) · [Open source notebook](../notebooks/06_dashboard_export.ipynb) · [Existing Google Sheets workbook](https://docs.google.com/spreadsheets/d/1Eg8WXpafT1n4bOWKCfnch2Eg_3ggpHsYRQIsYJcuyfw/edit)

## 1. Critical Google Sheets import blocker

The existing workbook `Findex Indonesia 2024 — Dashboard Data` currently contains one tab, `KPI_Aggregates`, with numeric values misparsed under `in_ID` locale. Example: the original survey-weighted account ownership rate for age 15–24 is **61.99266284**, but the existing tab stores **6199266284**. The weighted numerator and denominator fields are also affected. **Do not connect this tab to Looker Studio. Changing its number display format alone does not repair the values.**

Safe recovery on **the same workbook**:
1. Leave the old `KPI_Aggregates` tab as a clearly named archive (`ARCHIVE_KPI_BROKEN_LOCALE_DO_NOT_USE`) or hide it, rather than deleting without a backup.
2. Open **File → Settings → Locale**. Set **United States** for imports of CSV using periods as decimals, then save. After importing, verify **actual stored numeric values**, not just the number format.
3. In Google Sheets choose **File → Import → Upload**, select each **approved aggregate CSV** from the private dashboard exports folder (download the CSV from Drive temporarily if the importer needs a local file), choose **Insert new sheet(s)** (not Replace current sheet), and confirm CSV separator is **comma**.
4. Rename the six resulting tabs exactly as below, then **check national `account = 56.328`, `anydigpayment = 42.693`, and all `rate_pct` between 0 and 100**. If any field is interpreted as billions, delete the newly imported broken tab and reimport correctly. Do not correct individual values manually.
5. Do not import `integrated_respondents_private.csv`, original ZIP, respondent-level CSV, or `dashboard_all_kpis.csv` as the primary scorecard source. The combined KPI table duplicates some metrics across pages by design.

## 2. Import these six approved dashboard CSVs

**Source folder:** `MyDrive/Financial_Inclusion_Private/dashboard_exports/`

| CSV source | Google Sheets tab | Rows | Dashboard owner |
|---|---|---:|---|
| `dashboard_page1_overview.csv` | `01_Overview` | 6 | Rafa |
| `dashboard_page2_inclusion_segments.csv` | `02_Inclusion_Gaps` | 17 | Rafa |
| `dashboard_page2_gap_summary.csv` | `02_Gap_Summary` | 5 | Rafa |
| `dashboard_page3_digital_adoption.csv` | `03_Digital` | 100 | Mutia |
| `dashboard_page3_gap_summary.csv` | `03_Digital_Gaps` | 4 | Mutia |
| `dashboard_page4_financial_barriers.csv` | `04_Barriers` | 6 | Mutia |

Other Notebook 06 outputs—`dashboard_export_quality_checks.csv` (**12/12 PASS**), `dashboard_data_dictionary.csv` and `dashboard_export_manifest.json`—are review materials; keep them private and consult them when validating the dashboard.

**Required validation after import:** `rate_pct` must be numeric and from 0 to 100. `numerator_wgt` and `denominator_wgt` must remain nonnegative decimals (not locale-inflated integer strings); check `100 * numerator_wgt / denominator_wgt ≈ rate_pct` on sample rows. Verify `n_valid`, sample size warnings, one row per metric/dimension/category, and correct category ordering. Sheets locale changes affect the whole workbook; coordinate before modifying the shared workbook.

## 3. Dashboard implementation — separate ownership without conflicting edits

Create **one shared Looker Studio report with four pages**. Rafa is the integration owner and manages shared data-source connections, global theme, navigation, report access and final QA. Mutia builds only Pages 3 and 4 in that report after Rafa has connected the six verified tabs. Agree on a shared style: dark-navy headings, blue/teal charts, consistent font, caption `Indonesia · Survey 2024 · Weighted rate (%)`, footnote on descriptive survey interpretation. Use different pages for simultaneous editing; avoid both editors changing shared theme/data sources at the same time.

### Rafa — Page 1: Financial Inclusion Overview

**Data:** `01_Overview`. Use **six national scorecards**:
- Any account **56.33%**; financial institution account **52.39%**; mobile money account **22.01%**.
- Digital payment use **42.69%**; savings **52.99%**; borrowed **47.64%**.

Add a simple rate comparison chart with metric labels, non-additive explanatory note, and clear survey-year/source caption. Filter each scorecard to one `metric` and `dimension = national`.

### Rafa — Page 2: Inclusion Gaps

**Data:** `02_Inclusion_Gaps` + `02_Gap_Summary`. Use separate bar charts by income quintile, education, age, gender and residence, with `sort_order` ordering. Suggested gap annotations: tertiary vs primary **47.97 pp** (tertiary n=41: caution), Q5 vs Q1 **31.58 pp** (separate from maximum observed Q5 vs Q3 **31.80 pp**), ages 25–34 vs 55+ **30.62 pp**, female–male **3.39 pp**, urban–rural **0.64 pp**. No causal claims or statistical-significance claims.

### Mutia — Page 3: Digital Finance Adoption

**Data:** `03_Digital` + `03_Digital_Gaps`. Start with five national metric scorecards: internet use **70.46%**, digital payment **42.69%**, mobile money **22.01%**, saved **52.99%**, borrowed **47.64%**. Add two segment charts for digital payment by internet usage and income quintile; additional gender/age/education/residence views may be organized into separate charts. Highlight internet-user gap **36.16 pp** and income Q5–Q1 gap **33.00 pp**, with noncausal wording. Use segment-specific `metric = anydigpayment` and a single `dimension` per chart.

### Mutia — Page 4: Financial Barriers

**Data:** `04_Barriers`. Build a horizontal bar chart sorted by `rank`, using Indonesian labels. Values: not enough money **63.76%**; family member already has an account **52.28%**; high fees **51.54%**; too far away **39.74%**; missing documents **33.38%**; trust **17.78%**. Add caption: `Eligible: account_fin = 0 (n=504), valid per-item Yes/No denominators (n=484–502); multiple-response questions`. Do not sum to 100%.

## 4. Shared dashboard QA checklist (both owners)

- [ ] All six imported tabs contain the expected row counts, labels, and numeric values.
- [ ] Every national rate matches Notebook 03/06 to at least two decimals.
- [ ] Dashboard shows rates on a 0–100 scale with a `%` suffix; do not apply built-in percent format to raw 56.33 (which would display 5,633%). Instead use decimal formatting with suffix or a calculated `rate_pct / 100` field for percent formatting.
- [ ] Do not use `SUM(rate_pct)` or `AVG(rate_pct)` across categories, pages or different indicators. Fixed metric/dimension/category filters are mandatory for scorecards.
- [ ] Income and age categories sort via `sort_order`, not alphabetically.
- [ ] No multi-dimensional filter combinations (gender × income) from one-dimensional aggregates.
- [ ] `small_sample_warning` is respected; tertiary education group `n=41` is marked as cautious.
- [ ] The four pages explain survey year, weights, respondent counts and descriptive limitations.
- [ ] Google Sheets and Looker Studio sharing permissions allow both team members to edit safely.
- [ ] Final screenshots, report link and QA notes are added to GitHub `dashboard/README.md` and the main README only after actual publication.

**Privacy:** Never upload source respondent-level data or the raw World Bank ZIP to Google Sheets, Looker Studio or GitHub. Dashboard completion and publication remain separate from the successful Notebook 06 execution.
