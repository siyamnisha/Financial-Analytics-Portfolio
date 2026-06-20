# Monthly Analytics-Ready Dataset — Grameenphone Ltd. (DSE: GP)

**FIN 4333 Financial Analytics — Team Hemisphere**

A reproducible data pipeline that builds a clean, monthly, analytics-ready panel for Grameenphone Ltd. (DSE: GP) by combining daily stock prices, audited annual firm fundamentals, and macroeconomic indicators into a single 60-row dataset (Jan 2020 – Dec 2024).

[**View the live project page →**](https://your-username.github.io/your-repo-name/)

---

## What this is

Three very different data sources — daily market prices, annual financial statements, and annual macro indicators — rarely arrive in a shape that's ready for modelling. This project documents, end-to-end, how they were collected, cleaned, aligned to a common monthly frequency, merged, and quality-checked, with every step logged and every value traceable back to its source.

| | |
|---|---|
| **Company** | Grameenphone Ltd. (DSE: GP) |
| **Coverage** | January 2020 – December 2024 |
| **Frequency** | Monthly (60 rows) |
| **Variables** | 12 (identifiers, price/return, 3 firm fundamentals, 2 macro indicators) |
| **Quality checks** | 15 / 15 PASS |

## Repository structure

```
Project_1a_Team_Hemisphere/
├── raw_data/                  Unmodified source files
│   ├── stock/                 Daily price history (investing.com)
│   ├── firm_reports/          Audited annual reports 2020-2024 (PDF) + extracted CSV
│   └── macro_api_raw/         Cached World Bank API responses (JSON)
├── processed_data/            Intermediate cleaned tables (per source, pre-merge)
├── final_data/                final_monthly_dataset.csv — the analytics-ready output
├── notebooks/                 project_1_pipeline.ipynb — the full, documented pipeline
├── logs/                      source_log.csv, quality_check_sheet.csv, screenshots
└── outputs/                   data_dictionary.csv, overview_chart.png, project_memo.docx
```

## Data sources

| Component | Source | Notes |
|---|---|---|
| Stock — daily prices | investing.com, Grameenphone Historical Data | 1,163 trading days, resampled to month-end |
| Firm — Revenue, Total Assets, EPS | Grameenphone audited Annual Reports 2020–2024 | Cross-checked against AR2024 Table-1 (p.89) |
| Macro — GDP growth | World Bank API, `NY.GDP.MKTP.KD.ZG` (Bangladesh) | Fiscal-year basis, mapped to calendar year |
| Macro — Inflation (CPI) | World Bank API, `FP.CPI.TOTL.ZG` (Bangladesh) | Live API call, cached JSON fallback retained |

## Pipeline overview

1. **Import & clean** the daily stock file — parse dates, coerce prices, drop bad/duplicate rows, sort ascending.
2. **Resample** daily closes to month-end prices and compute monthly returns.
3. **Load annual firm variables** (Revenue, Total Assets, EPS) from the audited reports.
4. **Retrieve macro indicators** from the World Bank API; persist the raw JSON response.
5. **Align** annual firm and macro values onto monthly rows by calendar year (left-merge on `year`).
6. **Merge** all components into one ordered monthly table.
7. **Run 15 automated quality checks** and save the final CSV, data dictionary, and source log.
8. **Generate** the overview chart and a Word project memo summarizing the build.

The full step-by-step build, with before/after explanations for every transformation, is in [`notebooks/project_1_pipeline.ipynb`](Project_1a_Team_Hemisphere/notebooks/project_1_pipeline.ipynb). A headless `pipeline.py` reproduces the identical workflow.

## Key modelling decision: aligning annual data to monthly rows

The dataset is monthly, but firm and macro variables are reported annually. Each annual value is repeated across every month of its calendar year — e.g., all twelve 2023 rows carry the same 2023 Revenue, Total Assets, EPS, GDP growth, and inflation figures. This is a deliberate left-merge on the `year` key, documented in the data dictionary and memo.

## Data quality

All 15 automated checks pass:

- 60/60 monthly rows, one per month, continuous and duplicate-free (Jan 2020 – Dec 2024)
- `month_end_price` is missing only for **April 2020**, when the DSE suspended all trading (26 Mar – 31 May 2020, COVID-19) — a true "no trade" state, preserved rather than imputed
- `monthly_stock_return` is `NaN` for Jan-2020 (no prior month), Apr-2020 (no price), and May-2020 (prior month is `NaN`)
- All firm and macro columns are fully populated after alignment
- No extreme monthly returns (`|r| < 0.50`); EPS within a plausible band

See [`logs/quality_check_sheet.csv`](Project_1a_Team_Hemisphere/logs/quality_check_sheet.csv) for the full check-by-check log and [`outputs/data_dictionary.csv`](Project_1a_Team_Hemisphere/outputs/data_dictionary.csv) for variable-level definitions, units, and sources.

## Reproducing this

```bash
# clone the repo, then from the project root:
pip install -r requirements.txt        # pandas, numpy, requests, matplotlib, python-docx
jupyter notebook notebooks/project_1_pipeline.ipynb
# Kernel → Restart & Run All rebuilds every output from raw_data/
```

The macro step calls the live World Bank API and falls back to the cached raw JSON in `raw_data/macro_api_raw/` if offline, so the run is reproducible without an internet connection.

## Team Hemisphere

This project was completed for the Financial Analytics course at United International University. An AI-use disclosure document accompanies the formal submission.

## License

Educational coursework project. Raw annual report PDFs and stock data are the property of their respective sources (Grameenphone Ltd., investing.com, World Bank) and are included here for reproducibility of academic work only.
