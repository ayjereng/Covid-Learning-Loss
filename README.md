# COVID-19 Learning Loss in Bay Area Schools

Can school-level demographic factors predict which Bay Area schools were hit hardest by COVID-19?

---

## Overview

This project analyzes math learning loss across Bay Area public schools by comparing California CAASPP assessment scores from 2019 (pre-pandemic) to 2023 (recovery period). We engineer school-level demographic features from California Department of Education data and train regression models to predict school-level score decline.

**Finding:** School demographics explain only about 20% of variance in learning loss. The pandemic's impact did not simply follow pre-existing demographic lines -- district-level policy decisions were the primary driver.

---

## Research Question

> Can school-level demographic composition help predict which schools saw the greatest decline in math proficiency between 2019 and 2023?

---

## Data Sources

All data is publicly available from the California Department of Education:

- **CAASPP Research Files**: [cde.ca.gov/ta/tg/ca/caasppresearch.asp](https://www.cde.ca.gov/ta/tg/ca/caasppresearch.asp)
  - `sb_ca2019_all_csv_v4.txt` — 2019 test results by school/grade/subgroup
  - `sb_ca2023_all_csv_v1.txt` — 2023 test results by school/grade/subgroup
  - `sb_ca2019entities_csv.txt`, `sb_ca2023entities_csv.txt` — school metadata
  - `StudentGroups.txt` — demographic ID lookup table
  - `Tests.txt` — test subject lookup table

> Data files are not included in this repo due to size. Download from the CDE link above and place in the project root directory.

---

## Methods

**Feature Engineering**
- Filtered to 9 Bay Area counties and mathematics assessments only
- Created unique 14-digit school identifiers (County + District + School Code)
- Computed percentage of each demographic subgroup per school, normalized by total enrollment
- Target variable: `Learning_Loss = score_2023 - score_2019`

**Features**
15 demographic subgroups from 2019 covering disability status, socioeconomic status, English language fluency, race/ethnicity, and gender

**Models**
Linear Regression, Random Forest, XGBoost, Gradient Boosting with 5-fold cross-validation

---

## Key Findings

- The majority of Bay Area schools saw lower math scores in 2023 than 2019
- Pre-COVID baseline score is the strongest predictor -- schools that started higher tended to fall further
- No single demographic factor dominates, which explains the low overall R²
- The feature ceiling suggests missing drivers: how long districts stayed remote, chronic absenteeism rates, per-pupil spending on recovery programs, and teacher turnover

---

## Limitations

- No 2020-21 data: testing was suspended at peak COVID
- School-level averages mask within-school variation
- CAASPP suppresses results for subgroups with fewer than 11 students, causing NaN values in sparse demographics

