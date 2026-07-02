# Fatal Force in America: US Police Shootings Analysis (2015–2024)

A multi-dataset data analysis project examining fatal shootings by on-duty US police
officers, built in Python with pandas and interactive Plotly visualisations in Jupyter.

The analysis combines the Washington Post's Fatal Force database with US Census
demographic data and RAND firearm ownership estimates to move beyond raw counts —
adjusting for population to compare states and racial groups fairly, and testing
whether state gun ownership levels relate to how often suspects are armed.

---

## Data Sources

| Dataset | Source | Used for |
|---|---|---|
| Fatal police shootings, 2015–2024 | [Washington Post Fatal Force database](https://github.com/washingtonpost/data-police-shootings) (export dated 2026-06-25) | Core incident records: date, location, demographics, armed status |
| Population by race and state | US Census Bureau, ACS 2022 5-year estimates via the [Census API](https://www.census.gov/data/developers/data-sets.html) (tables B02001, B03002) | Per-capita rate denominators; minority share by state |
| Household firearm ownership by state | [RAND State-Level Estimates of Household Firearm Ownership](https://www.rand.org/pubs/tools/TL354.html) (TL-354, 2016 estimates) | Gun ownership vs. armed-incident correlation |
| State populations | [jakevdp/data-USstates](https://github.com/jakevdp/data-USstates) | State-level incidents-per-million choropleth |
| US city coordinates | [kelvins/US-Cities-Database](https://github.com/kelvins/US-Cities-Database) | Geocoding cities for the incident map |

**Scope note:** the Washington Post database records fatal **shootings by on-duty
officers** only — deaths in custody, off-duty incidents, and other causes are not
included. Records listing multiple races are grouped as *Mixed*; a substantial share
of records have unknown race and are excluded from race-based analysis.

---

## Key Questions Explored

- Has the number of fatal police shootings changed over time, and is there a trend?
- How do fatalities break down by gender, age, and race?
- Which states have the most incidents — and does the ranking change once adjusted
  for population?
- How do per-capita fatality rates compare across racial groups within each state,
  using each group's own population as the denominator?
- Where do incidents concentrate at city level?
- Do states with higher household gun ownership see a higher share of incidents
  where the suspect was armed?

---

## Analysis & Visualisations

**Trends over time**
- Monthly fatalities line chart (2015–2024) with linear trend line and centred
  12-month rolling average
- Monthly deaths by race as multi-series line charts

**Demographics**
- Gender breakdown (donut chart)
- Age distribution by gender: grouped bar chart by age band, plus histogram + KDE
  panels for male and female fatalities
- Racial breakdown donut with small-category handling (threshold-filtered labels,
  footnoted percentages for Mixed and Other)

**Geography**
- Choropleth of incident counts by state
- Choropleth of incidents **per million residents** by state — a materially
  different ranking from the raw counts
- Scatter-map of incidents by city (marker size and colour scaled to count)

**Race-adjusted rates** (Census integration)
- Per-capita fatality rates by race and state, using each racial group's ACS
  population as the denominator (`rate_per_million`)
- Faceted bar charts of the top 12 states ranked by overall per-capita rate
- Minority population share by state derived from the Census pull

**Armed status & gun ownership** (RAND integration)
- Armed / Unarmed / Unknown classification from the raw `armed` field
- Per-state armed-vs-unarmed breakdowns, faceted and ranked by household firearm
  ownership rate
- Scatter plot of household gun ownership vs. share of incidents classified as
  armed, with OLS trend line and a ranked table of the most aligned states

---

## Key Findings

<!-- Fill these in from the notebook outputs, e.g.: -->
- [Trend: direction and rough magnitude of the monthly slope]
- [Per-capita vs. raw-count state rankings: which states swap in/out of the top 12]
- [Race-adjusted rates: the headline disparity, with the per-million figures]
- [Gun ownership vs. armed share: strength/direction of the relationship]

---

## Tech Stack

- **Python 3.12**, Jupyter Notebook
- **pandas** — cleaning, merging five heterogeneous datasets, aggregation
- **Plotly** — interactive charts: choropleths, scatter-map, faceted bars,
  subplot + table composites, OLS trendlines
- **matplotlib** — time series, histograms, KDE, donut charts
- **numpy / scipy** — trend fitting, kernel density estimation
- **statsmodels** — OLS trendline backend for Plotly
- **requests + python-dotenv** — Census API access with key management
- **openpyxl** — reading the RAND `.xlsx` estimates

---

## Setup

```bash
git clone https://github.com/LegradiK/us_police_incidents_analysis.git
cd us_police_incidents_analysis
python -m venv venv
source venv/bin/activate
pip install pandas plotly matplotlib seaborn scipy numpy statsmodels \
            requests python-dotenv openpyxl jupyter
jupyter notebook 2015_2024_us_police_shooting_report_analysis.ipynb
```

**Census API key:** register for a free key at
[api.census.gov](https://api.census.gov/data/key_signup.html) and place it in a
`data.env` file in the project root:

```
US_CENSUS_KEY=your_key_here
```

After the first successful run the Census results are cached to CSV, so subsequent
runs (and the Voilà dashboard) work without hitting the API.

**RAND data:** download the TL-354 spreadsheet from the link above and place
`TL-354-State-Level Estimates of Household Firearm Ownership.xlsx` in the project
root.

### View as a dashboard (recommended)
 
The notebook is designed to be viewed with [Voilà](https://voila.readthedocs.io/),
which renders it as a clean, interactive dashboard — charts and commentary only,
no code cells:
 
```bash
pip install voila
voila 2015_2024_us_police_shooting_report_analysis.ipynb
```
 
This opens the dashboard in your browser at `http://localhost:8866`. All Plotly
charts remain fully interactive (hover, zoom, pan). Run the notebook once in
Jupyter first so the Census cache files are generated — after that, Voilà loads
without needing an API key.


---

## Project Structure

```
us_police_incidents_analysis/
│
├── 2026-06-25-washington-post-police-shootings-export.csv   # Washington Post incident data
├── 2015_2024_us_police_shooting_report_analysis.ipynb       # Main analysis notebook
├── TL-354-State-Level Estimates of Household Firearm Ownership.xlsx
├── data.env                                                 # Census API key (not committed)
├── census_state_race_2022.csv                               # Cached Census pull (auto-generated)
├── census_df_2022.csv                                       # Cached Census pull (auto-generated)
├── README.md
│
└── old_data_2015_2017/                                      # Earlier 2015–2017 analysis
    ├── Deaths_by_Police_US.csv
    ├── Median_Household_Income_2015.csv
    ├── Pct_Over_25_Completed_High_School.csv
    ├── Pct_People_Below_Poverty_Level.csv
    ├── Share_of_Race_By_City.csv
    └── us_police_incidents_analysis.ipynb
```

---

## Author

**LegradiK**
[GitHub](https://github.com/LegradiK) · [Portfolio](https://legradik.github.io)