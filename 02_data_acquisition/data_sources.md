# Data Sources — US Diabetes Health Disparities

---

## CDC PLACES — Local Data for Better Health, County Data (2025 Release)

### Provenance
- **Organization:** CDC, Division of Population Health, Epidemiology and Surveillance Branch
- **Version / Release Year:** 2025 release
- **Date Downloaded:** July 6, 2026
- **URL:** https://data.cdc.gov/500-Cities-Places/PLACES-Local-Data-for-Better-Health-County-Data-20/swc5-untb

### Content
- **What it measures:** Model-based county estimates for chronic disease outcomes and risk behaviors
- **Geographic level:** County (50 states + DC)
- **Time period:** Based on 2023 BRFSS data (35 measures) and 2022 BRFSS data (5 measures)
- **Unit of analysis:** County

### Access
- **Download method:** CSV download from CDC Data Portal (data.cdc.gov)
- **Local filename(s):** places_county_2025.csv
- **Registration required:** No

### Relevance to This Project
- **Variables used:** Diagnosed diabetes prevalence, obesity, physical inactivity
- **Connects to:** RQ1 (prevalence by geography), RQ2 (outcome distribution)

### Known Limitations
- Model-based estimates, not direct measurement
- Small area model cannot detect effects of local interventions; not suitable for program or policy evaluation
- Small counties may have wider confidence intervals

### Citation
- Centers for Disease Control and Prevention. PLACES: Local Data for Better Health, County Data 2025 Release. Atlanta, GA: CDC; 2025. https://www.cdc.gov/places


### Data Dictionary

| Column | Description | Type |
|--------|-------------|------|
| Year | Year of data | Text |
| StateAbbr | State abbreviation | Text |
| StateDesc | State name | Text |
| LocationName | County name | Text |
| DataSource | Data source | Text |
| Category | Topic category | Text |
| Measure | Measure full name | Text |
| Data_Value_Unit | Unit of measurement (e.g., %) | Text |
| Data_Value_Type | Crude or age-adjusted prevalence | Text |
| Data_Value | Estimate value | Number |
| Data_Value_Footnote_Symbol | Footnote symbol | Text |
| Data_Value_Footnote | Footnote text | Text |
| Low_Confidence_Limit | Lower bound of confidence interval | Number |
| High_Confidence_Limit | Upper bound of confidence interval | Number |
| TotalPopulation | Total county population (2023 Census estimates) | Number |
| TotalPop18plus | Population aged 18 and older | Number |
| LocationID | County FIPS code (stored as Text) | Text |
| CategoryID | Category identifier | Text |
| MeasureId | Measure identifier | Text |
| DataValueTypeID | Data value type identifier | Text |
| Short_Question_Text | Measure short name | Text |
| Geolocation | Latitude/longitude of county centroid | Point |

---

---

## Census / ACS — Race, Poverty, and Income (2023 5-Year Estimates)

### Provenance
- **Organization:** US Census Bureau
- **Version / Release Year:** 2023 ACS 5-Year Estimates
- **Date Downloaded:** July 7, 2026
- **URL:** https://api.census.gov

### Content
- **What it measures:** County-level demographic, income, and poverty estimates
- **Geographic level:** County (50 states + DC)
- **Time period:** 2019-2023 (5-year pooled estimates)
- **Unit of analysis:** County

### Access
- **Download method:** Census API via Python census library
- **Local filename(s):** census_race_2023.csv, census_poverty_2023.csv,
  census_income_2023.csv
- **Registration required:** Yes — free API key from api.census.gov

### Relevance to This Project
- **Variables used:** Race counts by county (B02001), percent below poverty
  level (S1701), median household income (B19013)
- **Connects to:** RQ1 and RQ2 — demographic and socioeconomic variables
  for disparity analysis

### Known Limitations
- 5-year estimates reduce margin of error for small counties but
  represent a pooled time period, not a single year
- Race and ethnicity are separate Census concepts — Hispanic/Latino
  requires a separate pull from B03003 (to be added)
- Margin of error not captured in current pull — small counties may
  have unreliable estimates
- Race category definitions may not align exactly with health data sources

### Citation
- US Census Bureau. American Community Survey 5-Year Estimates, 2023.
  Tables B02001, S1701, B19013. Retrieved via Census API, July 2026.
  https://api.census.gov

### Data Dictionary

| Column | Description | Type |
|--------|-------------|------|
| NAME | County and state name | Text |
| pop_total | Total county population | Number |
| pop_white | Population — White alone | Number |
| pop_black | Population — Black or African American alone | Number |
| pop_aian | Population — American Indian and Alaska Native alone | Number |
| pop_asian | Population — Asian alone | Number |
| pop_nhpi | Population — Native Hawaiian and Pacific Islander alone | Number |
| pop_multirace | Population — Two or more races | Number |
| pop_poverty_total | Total population for poverty determination | Number |
| pop_below_poverty | Population below poverty level | Number |
| pct_below_poverty | Percent below poverty level | Number |
| median_household_income | Median household income (past 12 months) | Number |
| LocationID | County FIPS code — join key to PLACES data | Text |


---

## NCHS Urban-Rural Classification Scheme for Counties (2023)

### Provenance
- **Organization:** CDC National Center for Health Statistics (NCHS)
- **Version / Release Year:** 2023 scheme, released January 2025
- **Date Downloaded:** July 7, 2026
- **URL:** https://www.cdc.gov/nchs/data_access/urban_rural.htm

### Content
- **What it measures:** Six-level urban-rural classification for all US counties
- **Geographic level:** County
- **Time period:** Based on 2023 OMB delineations and 2022 population estimates
- **Unit of analysis:** County

### Access
- **Download method:** CSV download from CDC NCHS website
- **Local filename(s):** NCHSurb-rural-codes.csv
- **Registration required:** No

### Relevance to This Project
- **Variables used:** CODE2023 (urban_rural_code), text label (urban_rural)
- **Connects to:** RQ1 — geographic dimension of disparity analysis

### Known Limitations
- 16 counties have missing codes and are excluded from the classification
- Classification reflects 2023 OMB delineations — may not reflect
  recent population shifts

### Citation
- National Center for Health Statistics. NCHS Urban-Rural Classification 
  Scheme for Counties. Atlanta, GA: CDC; 2025. 
  https://www.cdc.gov/nchs/data_access/urban_rural.htm