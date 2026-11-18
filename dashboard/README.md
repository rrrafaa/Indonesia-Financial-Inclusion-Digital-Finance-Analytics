# Looker Studio dashboard

**Project owners:** Rafa and Mutia.

- **Rafa:** Page 1 — Financial Inclusion Overview; Page 2 — Demographic & Income Inclusion Gap.
- **Mutia:** Page 3 — Digital Finance Adoption; Page 4 — Financial Barriers.
- **Together:** Notebook 06 dashboard export, review, and publishing.

**Status (18 November 2026):** Notebook 03 (14/14 checks), Notebook 04 (140/140 KPI checks), and Notebook 05 (100 digital KPI, 6 financial-barrier checks, 11 overall checks) were run successfully. Notebook 06 exists on GitHub **but has not yet been executed**; Looker Studio dashboard is not yet published.

## Run Notebook 06

[Open Notebook 06 in Google Colab](https://colab.research.google.com/github/rrrafaa/Indonesia-Financial-Inclusion-Digital-Finance-Analytics/blob/main/notebooks/06_dashboard_export.ipynb)

Run all cells using the same Google account / private Drive used in 03–05. The notebook requires validated outputs from all three notebooks in `MyDrive/Financial_Inclusion_Private/processed/`. It creates private `MyDrive/Financial_Inclusion_Private/dashboard_exports/` with:
- `dashboard_page1_overview.csv` — national inclusion card metrics.
- `dashboard_page2_inclusion_segments.csv` — 17 group rows for account ownership.
- `dashboard_page3_digital_adoption.csv` — 100 digital KPI group/national rows.
- `dashboard_page4_financial_barriers.csv` — 6 barriers with valid denominator metadata.
- `dashboard_page2_gap_summary.csv` and `dashboard_page3_gap_summary.csv`.
- `dashboard_all_kpis.csv`, `dashboard_data_dictionary.csv`, `dashboard_export_quality_checks.csv`, `dashboard_export_manifest.json`.

## Connect to Google Sheets and Looker Studio

Import only aggregate CSVs to separate Sheets tabs after reviewing quality checks. Use one metric + one dimension/category per chart; percentages already range from **0 to 100** and should not be SUM/AVG aggregated. The tables **do not** support combined demographic filters (such as gender and income simultaneously). For barriers, valid denominator means *Yes/No responses among 504 eligible financial institution non-account holders*, with per-question n varying. No time series, causal inference, or provincial ranking is supported.

**Privacy:** Never publish private respondent-level files, original ZIP or raw microdata in the spreadsheet or GitHub.