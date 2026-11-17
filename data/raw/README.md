# Raw data — World Bank Global Findex Indonesia (2024)

**Status:** Sumber data direferensikan, tetapi **CSV mikrodata tidak disimpan dalam repo publik ini**.

- **Dataset:** The Global Findex Database 2025 — Indonesia, survey year 2024
- **World Bank catalog:** https://microdata.worldbank.org/catalog/7917
- **Data dictionary:** https://microdata.worldbank.org/catalog/7917/data-dictionary/F1
- **Terms / Get Microdata:** https://microdata.worldbank.org/catalog/7917/get-microdata
- **Reference ID:** `IDN_2024_FINDEX_v02_M`
- **ZIP input:** `IDN_2024_FINDEX_v02_M_CSV.zip`
- **CSV inside ZIP:** `Findex_Microdata_2025_updateIndonesia.csv`
- **Verified data shape:** 1,068 records × 199 columns (in the project dataset).
- **SHA-256 ZIP:** `fc50f0a843e289a3b9784ac81dce1018a8195388608575e6c8315c195073a64c`
- **SHA-256 CSV:** `77a50e351c16946ad107c08494efe9e8972ba628168fa385b771695971710093`

## Why is the raw CSV missing?

The World Bank Microdata Library's terms include restrictions on redistribution without prior written permission. This is a public repository. Do not commit or share respondent-level microdata here unless you have verified and documented an applicable redistribution authorization.

## Local setup

1. Obtain the dataset from the official source and accept applicable conditions.
2. Place the original ZIP in `data/raw/IDN_2024_FINDEX_v02_M_CSV.zip` **locally only** (or keep it on private Google Drive for Colab).
3. Open `notebooks/01_data_profiling.ipynb`, run all cells.
4. Continue with `notebooks/04_eda_inclusion.ipynb`.
5. Confirm the SHA-256 matches this README; a mismatched checksum indicates a different dataset version.

`.gitignore` excludes raw datasets and respondent-level outputs by default.
