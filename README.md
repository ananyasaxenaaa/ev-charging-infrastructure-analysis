# EV Charging Infrastructure Analysis — India
**Dataset:** NDAP 8486 | **Period:** FY 2022-23 & FY 2023-24 | **States:** 18

## Project Overview
This project analyses Electric Vehicle (EV) charging infrastructure deployment and utilisation across Indian states using monthly data reported by electricity distribution companies (DISCOMs) to the National Data and Analytics Platform (NDAP).

The central research question is: **which states have demand for EV charging outpacing their current infrastructure, and should therefore be prioritised for expansion?**

---

## Repository Structure

| Folder | Contents |
|---|---|
| `data/raw/` | Original NDAP download files — unmodified |
| `data/cleaned/` | Cleaned datasets exported from Python |
| `notebooks/01_data_cleaning.ipynb` | Full data cleaning pipeline |
| `notebooks/02_eda_insights.ipynb` | EDA — stations, electricity, utilisation index |
| `notebooks/03_growth_analysis.ipynb` | Growth analysis and scatter plot |
| `excel/EV_analysis.xlsx` | Visual EDA — PivotTables and charts |
| `figures/` | Output charts from Python |


---

## Data Source
- **Platform:** [NDAP — National Data and Analytics Platform](https://ndap.niti.gov.in)
- **Dataset code:** 8486
- **Reported by:** Electricity DISCOMs across India
- **Granularity:** Monthly, by DISCOM and city/region
- **Raw rows:** 662 | **Cleaned rows:** 570

---

## Methodology

### Step 1 — Data Cleaning (Python)
The raw dataset had several quality issues addressed in `01_data_cleaning.ipynb`:
- Inconsistent city name formatting (spacing, capitalisation, mid-word breaks)
- Mislabelled rows (footnotes entered as data)
- Non-reporting rows (submitted with no numeric data)
- Column renaming for readability
- DISCOM column split into DISCOM + State for state-level analysis

### Step 2 — Exploratory Data Analysis (Excel + Python)
Visual EDA performed in `EV_analysis.xlsx` and `02_eda_insights.ipynb`:
- **Q1:** Which states have the highest average EV station count? → MAH and DELHI dominate
- **Q2:** Which states consume the most electricity? → DELHI leads at 252 MU
- **Q3:** How have these changed over time? → Stations +139%, electricity +176% year on year

### Step 3 — Utilisation Index
A derived metric defined as:

**U = Total EV Electricity Consumed (kWh) ÷ Total EV Station-Months**

Higher U means each station is serving more charging activity — demand outpacing infrastructure. States were tiered as High (>5,000), Medium (1,000–5,000), or Low (<1,000).

### Step 4 — Growth Analysis (Python)
Compared electricity consumption growth % vs EV station growth % between the two financial years per state. A positive gap means demand grew faster than infrastructure.

### Step 5 — Scatter Plot
Log-scale scatter of total stations vs total electricity per state to visually identify outliers — states sitting above the trend line consume more electricity than their station count predicts.

---

## Key Findings

| Finding | Detail |
|---|---|
| Sector growing rapidly | EV stations +139%, electricity +176% in one year |
| Infrastructure concentrated | MAH and DELHI hold ~70% of all reported stations |
| High utilisation states | HARYANA, RAJ, TN — demand severely outpacing infrastructure |
| Low utilisation states | MAH, KER, GUJ — infrastructure ahead of current demand |
| Expansion candidates | HARYANA and RAJ score high on utilisation index AND growth gap |

---

## Limitations
- Only two financial years of data — insufficient for robust statistical correlation or regression analysis
- Geography is at DISCOM region level, not official districts — some regions span multiple states
- ~8% of rows removed due to non-reporting — smaller DISCOMs may be underrepresented
- Growth rates for some states (BIHAR, JHARKHAND) are inflated due to near-zero 2022-23 baseline

---

## Future Work
If more years of data become available, the planned next steps are:
- **Pearson correlation** between utilisation index and external variables (state EV registrations, population density)
- **Linear regression** E = a + bN to model expected electricity consumption from station count
- **Residual analysis** to identify states consuming more or less electricity than their infrastructure predicts
- **Cross-dataset analysis** using NDAP's standardised LGD codes to join with census or economic data

---

## Tools Used
- Python 3 (pandas, matplotlib) — data cleaning and analysis
- Jupyter Notebooks (VS Code) — development environment
- Microsoft Excel — visual EDA and PivotTables

---

*Project done under the mentorship of Prof. Charu Sharma | Shiv Nadar University | Summer 2026*
