# Indonesia Financial Inclusion & Digital Finance Analytics

An end-to-end collaborative Data Analyst portfolio analyzing the **Global Findex Indonesia 2024** microdata (from the World Bank Global Findex Database 2025). Python (Colab/local) → validated survey-weighted metrics → Google Sheets / Looker Studio.

## Team ownership

| Owner | Scope | Notebook | Looker Studio |
|---|---|---|---|
| Person 1 (rrrafaa) | Quality profiling, demographic/financial-inclusion EDA, account gap, survey-weighted KPI | `01_data_profiling.ipynb`, `04_eda_inclusion.ipynb` | Pages 1–2 |
| Person 2 | Survey codebook, digital finance/barrier variables, related EDA and aggregation | `02_variable_mapping.ipynb`, `05_eda_digital_barriers.ipynb` (planned) | Pages 3–4 |
| Both | Shared cleaning, validation, export and review | `03_cleaning_integration.ipynb`, `06_export_dashboard.ipynb` (planned) | Integrated report |

## Project structure

```text
data/
  raw/README.md                      # raw source metadata, NOT the microdata
  processed/.gitkeep                 # outputs generated locally
notebooks/
  01_data_profiling.ipynb            # Person 1
  04_eda_inclusion.ipynb             # Person 1
reports/README.md
dashboard/README.md
requirements.txt
.gitignore
README.md
```

## How to run — Colab

1. Open each notebook directly from GitHub using **File → Open notebook → GitHub** and paste this repository URL.
2. Run all cells. The first data-loading cell will request the **original ZIP** (`IDN_2024_FINDEX_v02_M_CSV.zip`) if not found.
3. Run `01_data_profiling.ipynb` before `04_eda_inclusion.ipynb`. In a new Colab runtime, upload the ZIP again.
4. Check the outputs and sample-size warnings. Export only approved, aggregated findings to public artifacts.

## How to run — local

```bash
git clone https://github.com/rrrafaa/Indonesia-Financial-Inclusion-Digital-Finance-Analytics.git
cd Indonesia-Financial-Inclusion-Digital-Finance-Analytics
python -m venv .venv
# Windows: .venv\Scripts\activate
# macOS/Linux: source .venv/bin/activate
python -m pip install -r requirements.txt
jupyter lab
```

Download the microdata from the [World Bank catalog](https://microdata.worldbank.org/catalog/7917/get-microdata) under its applicable terms, place the original ZIP at `data/raw/IDN_2024_FINDEX_v02_M_CSV.zip` **on your own machine**. Do not commit it to a public repo.

## Data source and governance

- Indonesia, survey year 2024; uploaded version verified: 1,068 rows, 199 columns.
- The ZIP's SHA-256 is documented at [data/raw/README.md](data/raw/README.md).
- `wgt` is the survey weight. Use a weighted denominator over **valid answers only**. Keep unanswered/skip-logic values separate from 0/No.
- Cross-sectional associations are **not causal effects**; do not make province/time-series claims from this single-country, single-year file.
- No respondent-level data or respondent identifiers should be committed or shared publicly without permission. The `.gitignore` excludes raw and derived CSV files by default.
- Official [World Bank Global Findex](https://www.worldbank.org/en/publication/globalfindex) and [Microdata Library catalog](https://microdata.worldbank.org/catalog/7917).

## Git workflow

```bash
git fetch origin
git switch -c feat/person1-profiling-eda
# after running and reviewing notebooks
git add notebooks/ README.md requirements.txt
git commit -m "feat(eda): add person 1 data profiling and inclusion analysis"
git push -u origin feat/person1-profiling-eda
```

Create a pull request into `main`, request teammate review, merge only after validating the expected shapes and weighted metrics. **Never force-add ignored raw files.**

## Person 1 acceptance checks

- [ ] Original ZIP checksum and row/column counts match.
- [ ] Profile report includes schema, duplicates, missing values, categorical codes and survey-weight diagnostics.
- [ ] Account-rate EDA by gender, income quintile, education, age group, and urban/rural.
- [ ] Weighted rate is computed by valid-answer subgroup, not arithmetic average.
- [ ] Small-sample segments are flagged and no causal claims are made.
- [ ] Outputs are saved locally under `data/processed/` and are not pushed to GitHub.
- [ ] Teammate reviews the code and charts via Pull Request.
