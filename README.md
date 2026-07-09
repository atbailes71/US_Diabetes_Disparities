# US Diabetes Health Disparities Analysis

*Are diabetes outcomes distributed equally across race, income, and 
geography in the United States — and if not, by how much and where?*

---

## The Problem

Type 2 diabetes affects more than 37 million Americans, but that burden 
is not shared equally. County-level prevalence ranges from under 5% to 
over 27% — a gap that cannot be explained by chance. This project 
quantifies where those disparities are largest, which structural factors 
predict high-burden counties, and what the data implies for program 
prioritization and resource allocation.

---

## What This Project Demonstrates

| Competency | Demonstrated By |
|------------|----------------|
| Business needs assessment | Research questions translated into measurable metrics before touching data |
| Data acquisition and management | Four public datasets acquired via API and direct download, joined on FIPS code |
| Exploratory data analysis | Distribution analysis, correlation matrix, scatter plots across 2,956 counties |
| Disparity analysis | Rate ratios and absolute differences by income, urban/rural, and racial composition |
| Regression modeling | Linear regression (R²=0.925) and logistic regression (AUC up to 0.988) |
| Model validation | Residual plots, polynomial term for non-linearity, train/test split evaluation |
| Data governance | data_dictionary.md documenting all analytical decisions and limitations |
| Visualization | Choropleth maps, distribution charts, correlation heatmap, ROC curves |

---

## Research Questions

- **RQ1:** How does diabetes prevalence vary by race/ethnicity, income, 
  and geography across US counties?
- **RQ2:** Do diabetes outcomes differ across these groups beyond 
  prevalence alone?
- **RQ3:** What factors most strongly predict high diabetes burden 
  after controlling for confounders?

---

## Key Findings

**Income gradient:** Counties in the lowest income quintile average 
17.1% diabetes prevalence versus 11.0% in the highest, a rate ratio 
of 1.55 and an absolute gap of 6.1 percentage points.

**Urban/rural gradient:** Noncore rural counties average 14.6% versus 
11.6% in large central metro counties, a rate ratio of 1.26.

**Geographic clustering:** Mississippi (17.3%), West Virginia (17.0%), 
and Alabama (16.8%) are the highest-burden states. Vermont (9.6%) and 
New Hampshire (10.0%) are the lowest. The state-level gap of 7.7 
percentage points exceeds the income quintile gap.

**Racial composition:** County Black population share is the strongest 
racial predictor of diabetes prevalence (r=0.524). This is an 
ecological finding; it reflects structural patterns at the county 
level, not individual risk.

**Multivariate model:** After controlling for all predictors, high 
blood pressure prevalence (BPHIGH) is the strongest independent 
predictor of county diabetes burden. Poverty percentage outperforms 
median household income as the income measure. Urban/rural status 
becomes modest after income and poverty are controlled, supporting 
the hypothesis that income mediates much of the rural health penalty.

Hispanic population share shows a suppressor effect: its bivariate 
correlation with diabetes prevalence is near zero (r=0.015), but 
its standardized coefficient in the multivariate model is 0.596, the 
second strongest predictor. This is because pct_hispanic is negatively 
associated with BPHIGH, the model's strongest predictor, which masks 
its true relationship in a simple correlation.

**Structural prediction:** A logistic regression model using only 
demographic and socioeconomic variables (no health measures) correctly 
identifies high-burden counties with AUC of 0.871, confirming that 
diabetes burden is systematically distributed along structural lines.

---

## Data Sources

| Source | Content | Access |
|--------|---------|--------|
| CDC PLACES (2025) | County-level chronic disease prevalence | Direct download |
| Census ACS (2023) | Race, income, poverty by county | Census API |
| NCHS Urban-Rural Classification | Six-level urban/rural scheme | Direct download |
| NHANES | Clinical measures | Referenced in limitations |

---

## Project Structure

US_Diabetes_Disparities/
├── 01_business_needs/
│   └── analysis_plan.md
├── 02_data_acquisition/
│   ├── data_sources.md
│   ├── places_county_2025_filtered.csv
│   ├── census_race_2023.csv
│   ├── census_poverty_2023.csv
│   ├── census_income_2023.csv
│   ├── census_hispanic_2023.csv
│   └── merged_analysis_ready.csv
├── 03_analysis/
│   ├── 01_eda.ipynb
│   ├── 02_feature_transformation.ipynb
│   ├── 03_disparity_analysis.ipynb
│   └── 04_multivariate_analysis.ipynb
├── 04_reporting/
│   └── dashboard/
└── 05_governance/
└── data_dictionary.md

---

## Tools and Stack

Python (pandas, scikit-learn, matplotlib, seaborn, plotly) | 
SQL | Jupyter Notebooks | Power BI | GitHub

---

## Limitations

- PLACES estimates are model-based, not direct measurement
- Analysis is cross-sectional — findings are associational, not causal
- County-level ecological analysis — findings do not imply 
  individual-level relationships
- NHANES A1C control data was not available at county level; 
  comorbidity measures used as proxies for RQ2
- A small number of county-equivalents were excluded due to 
  FIPS code mismatches

---

## Documentation

- `01_business_needs/analysis_plan.md` — research questions, 
  metrics, analytical approach, and stakeholder framing
- `02_data_acquisition/data_sources.md` — full documentation 
  of all datasets including provenance, variables, limitations, 
  and citations
- `05_governance/data_dictionary.md` — analytical decisions, 
  variable definitions, exclusions, and assumptions

---

## Author

Adam Bailes, MPH | MS Data Science candidate, Boston University (Dec 2026)  
20+ years global health and nutrition experience across Sub-Saharan 
Africa and Southeast Asia  
adam.t.bailes@gmail.com | linkedin.com/in/adam-bailes-458a35b/