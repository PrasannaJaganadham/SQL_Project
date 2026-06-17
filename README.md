# COVID-19 Hospitalization & Mortality Analysis — San Francisco

A SQL-based analytical project examining COVID-19 hospitalization trends, mortality patterns, and testing outcomes in San Francisco hospitals from 2020 to 2024. Built to uncover relationships between ICU/Med-Surg patient load, demographic mortality risk, and testing volume — and to turn those patterns into concrete healthcare capacity recommendations.

## Overview

The COVID-19 pandemic put sustained pressure on hospital ICU and Med/Surg departments. This project integrates five years of hospitalization, testing, and mortality data into a single analytical model to answer three questions:

1. How did ICU and Med/Surg patient counts evolve over time, and what periods saw the sharpest changes?
2. How did mortality vary across age groups, and when did mortality spikes occur?
3. How do hospitalization rates, testing volume, and mortality trends relate to one another?

## Data Model

The database integrates six source tables into a unified analytical view:

- `archived_covid_19_icu` — daily ICU patient counts by hospital
- `archive_covid_19_med_sug` — daily Med/Surg (acute care) patient counts by hospital
- `covid_19_overtime` — daily positive/negative test counts
- Seven age-group mortality tables (`0_4`, `18_20`, `21_24`, `50_59`, `60_69`, `70_79`, `80_`) — combined into a single `combined_mortality` table via `UNION ALL`
- `date_table` — a shared date dimension joining all of the above by `Date_id`

## Key Techniques

- **CTEs and multi-table joins** to combine hospitalization, testing, and mortality data into one queryable structure
- **`UNION ALL`** to merge seven separate age-group mortality tables into a single `combined_mortality` table
- **Window functions (`LAG`)** to calculate month-over-month mortality changes and flag statistically unusual spikes (using a threshold of mean + 2 standard deviations)
- **Derived ratio metrics**, including an ICU-conversion ratio (ICU admissions ÷ positive tests) to measure how testing volume translated into severe outcomes
- **Aggregate functions** (`SUM`, `MAX`, `AVG`, `STDDEV`) for yearly and monthly trend analysis

## Key Findings

- ICU hospitalizations peaked in January 2021, with a clear seasonal decline through mid-2021 before a smaller rebound.
- The 80+ age group accounted for the large majority of COVID-19 deaths across the entire study period, far outweighing all other age groups combined.
- December 2020–January 2021 stood out as the sharpest mortality spike in the dataset, identified using window-function-based spike detection rather than manual inspection.
- 2022 recorded the highest combined ICU and Med/Surg hospitalization volume, while 2023–2024 showed a sustained decline in both hospitalizations and mortality.

## Recommendations

Based on the analysis, the report outlines five recommendations: scalable healthcare infrastructure that allows rapid conversion between Med/Surg and ICU capacity, targeted protective measures for patients aged 60+, continued investment in large-scale testing and surveillance, regularly updated predictive models to anticipate future demand, and public awareness campaigns on early testing and treatment.

## Tools Used

SQL · PostgreSQL · Docker (containerized database instance)

## Files

- `Project_Report.pdf` — full write-up including all queries, results tables, and analysis commentary
- Database schema diagram included in the report

---

*This project was completed as part of the MSc Data Science & Organisational Behaviour program at Burgundy School of Business.*
