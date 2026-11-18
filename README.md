# Indonesia Financial Inclusion & Digital Finance Analytics

**Data Analyst portfolio kolaborasi Rafa & Mutia** — analisis inklusi keuangan dan adopsi keuangan digital Indonesia menggunakan **World Bank Global Findex 2025, survei Indonesia tahun 2024**.

**Alur:** sumber resmi → Python / Google Colab → validasi dan cleaning bersama → eksplorasi berbobot (`wgt`) → tabel agregat tervalidasi → Google Sheets / Looker Studio.

> **Status 18 November 2026:** Notebook 01–05 tersedia di GitHub. Notebook 03: **14/14 QA PASS**, Notebook 04: **140/140 KPI cross-checks PASS**, dan Notebook 05: **100/100 KPI + 6/6 barrier cross-checks serta 11/11 QA PASS** berdasarkan hasil Google Colab. Notebook 06 telah dibuat dan siap dijalankan di Colab; ekspor dashboard dan publikasi Looker Studio belum dieksekusi.

## Tim dan tanggung jawab

| Anggota | Lingkup kerja | Notebook | Halaman dashboard |
|---|---|---|---|
| **Rafa** (`rrrafaa`) | Data profiling, kualitas data, financial inclusion, demographic/income gap, weighted KPI, interpretasi | [01 — Data Profiling](notebooks/01_data_profiling.ipynb), [04 — Inclusion EDA](notebooks/04_eda_inclusion.ipynb) | Page 1–2 |
| **Mutia** | Codebook dan variable mapping, digital finance, financial barriers, EDA digital dan rekomendasi | [02 — Variable Mapping](notebooks/02_variable_mapping.ipynb), [05 — Digital/Barriers EDA](notebooks/05_eda_digital_barriers.ipynb) | Page 3–4 |
| **Rafa + Mutia** | Cleaning, weighted KPI validation, integrasi, ekspor dashboard, cross-review | [03 — Cleaning Integration](notebooks/03_cleaning_integration.ipynb), [06 — Dashboard Export](notebooks/06_dashboard_export.ipynb) | Seluruh halaman |

## Struktur repository

```text
Indonesia-Financial-Inclusion-Digital-Finance-Analytics/
├── data/
│   ├── raw/
│   │   └── README.md                     # provenansi dan checksum; tidak menyimpan raw mikrodata
│   └── processed/
│       └── .gitkeep                     # CSV hasil proses tidak dipublish
├── notebooks/
│   ├── 01_data_profiling.ipynb          # Rafa — executed
│   ├── 02_variable_mapping.ipynb        # Mutia — source corrected; affected outputs need rerun
│   ├── 03_cleaning_integration.ipynb    # Rafa + Mutia — executed, 14/14 QA PASS
│   ├── 04_eda_inclusion.ipynb           # Rafa — executed, 140/140 KPI cross-checks PASS
│   ├── 05_eda_digital_barriers.ipynb    # Mutia — Colab executed, 100+6 validations PASS
│   └── 06_dashboard_export.ipynb        # Shared — available, requires first run
├── reports/
│   ├── README.md
│   ├── person1_quality_findings.md      # Rafa — original report filename retained
│   └── person1_eda_findings.md          # Rafa — integrated EDA report
├── dashboard/
│   └── README.md
├── requirements.txt
├── .gitignore
└── README.md
```

## Progress pekerjaan

| Tahap | Penanggung jawab | Status |
|---|---|---|
| 01 — Data Profiling | Rafa | **Selesai**, dieksekusi dan didokumentasikan |
| 02 — Variable Mapping | Mutia | **Kode tersedia**, mapping `fin11d/e/f` telah dikoreksi; output terkait perlu dijalankan ulang |
| 03 — Cleaning & Integration | Rafa + Mutia | **Selesai dijalankan**, checksum tervalidasi, 14/14 quality checks PASS |
| 04 — Financial Inclusion EDA | Rafa | **Selesai dijalankan memakai data terintegrasi**, 140/140 KPI cross-checks PASS |
| 05 — Digital Finance & Barriers EDA | Mutia | **Sudah dijalankan di Colab**, 100/100 KPI, 6/6 barrier dan 11/11 QA PASS; interpretasi diperbarui |
| 06 — Dashboard Export | Rafa + Mutia | **Notebook tersedia**, menunggu eksekusi dan audit hasil ekspor |
| Looker Studio | Rafa + Mutia | **Belum dibuat/dipublikasikan** |

**Catatan:** Lulusnya kode pengecekan otomatis tidak sama dengan validasi penuh terhadap desain survei atau signifikansi statistik. Interpretasi bersifat deskriptif; tinjau codebook, denominator, definisi KPI, dan ukuran kelompok saat peer review.

## Sumber dataset dan lisensi

- **Sumber:** World Bank Global Findex Database 2025, Indonesia survey year **2024**.
- **Katalog resmi:** https://microdata.worldbank.org/catalog/7917
- **Codebook:** https://microdata.worldbank.org/catalog/7917/data-dictionary/F1
- **Nama ZIP:** `IDN_2024_FINDEX_v02_M_CSV.zip`.
- **Nama CSV dalam ZIP:** `Findex_Microdata_2025_updateIndonesia.csv`.
- **Dimensi dataset:** **1.068 responden × 199 kolom**.
- **Provenansi dan hash SHA-256:** [data/raw/README.md](data/raw/README.md).
- **Akses dataset:** https://microdata.worldbank.org/catalog/7917/get-microdata

**Dataset mikro responden tidak dipublikasikan di GitHub**. Unduh resmi sesuai ketentuan World Bank, kemudian simpan ZIP di lokal atau folder Google Drive **privat**. File `.gitignore` mencegah commit umum untuk ZIP, CSV dan artefak tingkat responden. Jangan force-add.

## Menjalankan notebook di Google Colab

1. Buka notebook langsung dari GitHub menggunakan tombol **Open in Colab** di bawah atau gunakan menu **File → Open notebook → GitHub**.
2. Untuk Notebook **01/03**, unggah ZIP resmi yang kamu peroleh sendiri ketika diminta.
3. Jalankan Notebook **03** sampai ada `ALL INTEGRATION CHECKS PASSED.`, lalu simpan output privatnya di `MyDrive/Financial_Inclusion_Private/processed/`.
4. Jalankan Notebook **04** menggunakan Google Drive yang sama. Notebook ini akan otomatis mencari **empat file hasil Notebook 03**, tidak meminta ZIP mentah: `integrated_respondents_private.csv`, `dashboard_kpi_aggregates.csv`, `integration_quality_checks.csv`, `integration_manifest.json`.
5. Verifikasi pesan **`ALL 140 KPI CROSS-CHECKS PASSED.`**. Grafik dan lima file hasil analisis Rafa disimpan ke lokasi data olahan yang sesuai.
6. Notebook **05** sudah dijalankan dari output Notebook 03: **100/100 KPI**, **6/6 barrier**, dan **11/11 QA PASS**. Agregat digital Mutia tersimpan di folder processed privat.
7. Jalankan Notebook **06** menggunakan folder processed privat yang sama. Notebook 06 menggabungkan data agregat 03/04/05, memverifikasi ulang handoff, dan menyimpan file ke `MyDrive/Financial_Inclusion_Private/dashboard_exports/`. Jangan mengunggah mikrodata ke dashboard.

**Colab langsung:**
- [Rafa — Notebook 01](https://colab.research.google.com/github/rrrafaa/Indonesia-Financial-Inclusion-Digital-Finance-Analytics/blob/main/notebooks/01_data_profiling.ipynb)
- [Mutia — Notebook 02](https://colab.research.google.com/github/rrrafaa/Indonesia-Financial-Inclusion-Digital-Finance-Analytics/blob/main/notebooks/02_variable_mapping.ipynb)
- [Rafa + Mutia — Notebook 03](https://colab.research.google.com/github/rrrafaa/Indonesia-Financial-Inclusion-Digital-Finance-Analytics/blob/main/notebooks/03_cleaning_integration.ipynb)
- [Rafa — Notebook 04](https://colab.research.google.com/github/rrrafaa/Indonesia-Financial-Inclusion-Digital-Finance-Analytics/blob/main/notebooks/04_eda_inclusion.ipynb)
- [Mutia — Notebook 05](https://colab.research.google.com/github/rrrafaa/Indonesia-Financial-Inclusion-Digital-Finance-Analytics/blob/main/notebooks/05_eda_digital_barriers.ipynb)
- [Rafa + Mutia — Notebook 06](https://colab.research.google.com/github/rrrafaa/Indonesia-Financial-Inclusion-Digital-Finance-Analytics/blob/main/notebooks/06_dashboard_export.ipynb)

## Menjalankan secara lokal

```bash
git clone https://github.com/rrrafaa/Indonesia-Financial-Inclusion-Digital-Finance-Analytics.git
cd Indonesia-Financial-Inclusion-Digital-Finance-Analytics
python -m venv .venv
# Windows PowerShell: .\.venv\Scripts\Activate.ps1
# macOS/Linux: source .venv/bin/activate
python -m pip install -r requirements.txt
jupyter lab
```

Notebook 03: simpan ZIP asli di `data/raw/`, kemudian run all. Notebook 04 dan 05: gunakan output Notebook 03 di `data/processed/` atau Drive privat. Notebook 06: kumpulkan hasil agregat 03/04/05 dalam folder processed yang sama, kemudian run all. Notebook 02 memiliki path input Colab spesifik milik Mutia.

## Metodologi utama

- **Pembobot:** `wgt` adalah *survey sample weight*, bukan jumlah penduduk. Weighted rate (%) = `100 × SUM(wgt × indikator_1) / SUM(wgt responden valid)`.
- **Jawaban tidak valid dan skip logic:** tidak boleh diganti otomatis menjadi `No/0`; indikator harus mengikuti populasi dan coding pada codebook.
- **Hambatan rekening:** `fin11a`–`fin11f` ditanyakan pada responden **tanpa rekening lembaga keuangan** (`account_fin == 0`); jawaban valid adalah **1 = Ya**, **2 = Tidak**. Kode **3/4** tidak masuk denominator.
- **2024 barrier labels:** `fin11d` = tidak cukup uang, `fin11e` = anggota keluarga sudah punya rekening, `fin11f` = kurang percaya kepada lembaga keuangan.
- **Tidak ada analisis kausal atau time series:** dataset ini cross-sectional Indonesia 2024; tidak mendukung peta/ranking provinsi.
- **Batasan filter:** agregasi per-dimensi Notebook 03 tidak otomatis memungkinkan filter multidimensi gabungan. Gunakan Notebook 06 untuk tabel silang tambahan jika dashboard memerlukannya.

## Deliverable Notebook 06 dan dashboard

**Rafa:** Page 1 Financial Inclusion Overview dan Page 2 Inclusion Gap.  
**Mutia:** Page 3 Digital Finance Adoption dan Page 4 Financial Barriers.  
**Rafa + Mutia:** Notebook 06, review denominator/KPI, data export agregat, dashboard publishing, dashboard screenshots dan dokumentasi hasil.

Lihat [laporan QA Rafa](reports/person1_quality_findings.md), [laporan EDA Rafa](reports/person1_eda_findings.md), dan [rencana halaman dashboard](dashboard/README.md).

## Workflow GitHub

Gunakan branch fitur + Pull Request untuk perubahan berikutnya; hindari mengedit notebook `.ipynb` yang sama secara bersamaan.

```bash
git fetch origin
git switch main
git pull --ff-only origin main
git switch -c feat/dashboard-visual-review
# tambahkan dokumentasi atau tampilan dashboard (bukan data mentah)
git add README.md dashboard/ reports/
git commit -m "docs(dashboard): add validated visualization and review"
git push -u origin feat/dashboard-visual-review
```

Setelah review, merge PR ke `main`. **Jangan force-add ZIP/CSV mikrodata.**
