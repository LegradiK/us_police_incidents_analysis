# US Police Incidents Analysis

A multi-dataset data analysis project exploring patterns in US police fatalities from 2015 to 2024, using Python, pandas, and interactive Plotly visualisations in Jupyter notebooks.

---

## Overview

This project investigates the social and demographic factors surrounding police killings in the United States. It merges five datasets to explore relationships between fatalities and variables such as poverty rate, race, age, gender, mental health, armed status, and geography.

---

## Datasets

**Main dataset**

| Dataset | Description |
|---|---|
| `2026-06-25-washington-post-police-shootings-export.csv` | Washington Post police shootings database (2015–2024) |

**Legacy datasets (in `old_data_2015_2017/`)**

| Dataset | Description |
|---|---|
| `Deaths_by_Police_US.csv` | Records of individuals killed by police in the US (2015–2017) |
| `Median_Household_Income_2015.csv` | Median household income by city |
| `Pct_People_Below_Poverty_Level.csv` | Percentage of population below poverty line by city |
| `Pct_Over_25_Completed_High_School.csv` | High school graduation rates for adults over 25 by city |
| `Share_of_Race_By_City.csv` | Racial composition by city |

---

## Key Questions Explored

- Which cities and states have the highest number of police fatalities?
- How does poverty rate correlate with police killings?
- What is the racial breakdown of those killed, and does it vary by city?
- How do age and gender affect fatality patterns?
- What proportion of those killed showed signs of mental illness?
- What weapons were victims reported to be carrying?
- Has the number of police killings changed over time?

---

## Visualisations

**Geographic**
- Choropleth map of police killings by state
- Choropleth map of poverty rate by state (side-by-side comparison)
- Scatter mapbox of poverty rates at city level

**Demographics**
- Horizontal bar chart of fatalities by race with percentage of total
- Stacked bar chart showing mental health breakdown within each racial group
- KDE plots of age distribution by race
- Histogram and KDE of age group distribution
- Sunburst chart: gender → age group → manner of death

**Armed Status**
- Two-level sunburst: Armed vs Unarmed → weapon type breakdown
- Low-count weapons grouped into "Other" with footnote listing all items

**City Rankings**
- Top 10 cities by fatalities with rank, state abbreviation, count, and share of total
- Stacked bar chart showing racial composition of fatalities per city

**Time Series**
- Monthly fatalities line chart (2015–2020) with month/year x-axis
- Linear trend line and 12-month rolling average overlay

---

## Tech Stack

- **Python 3.12**
- **pandas** — data cleaning, merging, aggregation
- **Plotly** — interactive charts (sunburst, choropleth, scatter mapbox)
- **matplotlib** — static charts (bar, KDE, histogram, line)
- **seaborn** — jointplots and lmplots
- **scipy** — KDE (gaussian_kde)
- **numpy** — trend line fitting
- **Jupyter Notebook** — analysis environment

---

## Setup

```bash
git clone https://github.com/LegradiK/us_police_incidents_analysis.git
cd us_police_incidents_analysis
python -m venv venv
source venv/bin/activate
pip install pandas plotly matplotlib seaborn scipy numpy jupyter
jupyter notebook 2015_2026_us_police_shooting_report_analysis.ipynb
```

---

## Project Structure

```
us_police_incidents_analysis/
│
├── 2026-06-25-washington-post-police-shootings-export.csv   # Main dataset (Washington Post)
├── 2015_2026_us_police_shooting_report_analysis.ipynb       # Main Jupyter notebook
├── README.md
│
└── old_data_2015_2017/                                      # Original 2015–2017 datasets
    ├── Deaths_by_Police_US.csv
    ├── Median_Household_Income_2015.csv
    ├── Pct_Over_25_Completed_High_School.csv
    ├── Pct_People_Below_Poverty_Level.csv
    ├── Share_of_Race_By_City.csv
    └── us_police_incidents_analysis.ipynb
```

---

## Key Findings



---

## Author

**LegradiK**
[GitHub](https://github.com/LegradiK) · [Portfolio](https://legradik.github.io)