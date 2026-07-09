# Data Dictionary — US Diabetes Health Disparities

## Analytical Decisions

### Loving County, TX (FIPS 48301) — Excluded
- **Decision:** All rows for Loving County dropped from analysis
- **Reason:** Population under 50; all estimates suppressed by CDC
- **Rows affected:** 10 rows across DIABETES, OBESITY, LPA, BPHIGH, HIGHCHOL
- **Applied in:** 01_eda.ipynb

## Variable Definitions

[To be completed as analysis progresses]

### Crude Prevalence Selected Over Age-Adjusted Prevalence
- **Decision:** Analysis uses crude prevalence estimates throughout
- **Reason:** Consistent with CDC PLACES documentation for county-level 
  comparisons; age-adjusted prevalence is provided for trend comparisons 
  across time periods, not for geographic disparity analysis
- **Applied in:** 01_eda.ipynb — filter applied before pivot and all 
  subsequent analysis
- **Code:** df_crude = df_clean[df_clean['Data_Value_Type'] == 'Crude prevalence']

### Long to Wide Format Pivot
- **Decision:** Dataset pivoted from long format to wide format for 
  correlation analysis and joining to Census/ACS data
- **Reason:** Long format has one row per county per measure; wide format 
  has one row per county with each measure as a column, which is required 
  for correlation matrices and regression modeling
- **Applied in:** 01_eda.ipynb
- **Code:** df_wide = df_crude.pivot_table(index='LocationID', 
  columns='MeasureId', values='Data_Value').reset_index()

  ### Note — Loving County drop not included in saved filtered CSV
- places_county_2025_filtered.csv was saved before the null drop step
- Loving County rows are dropped at the start of 02_feature_transformation.ipynb
- All downstream analysis uses the cleaned data