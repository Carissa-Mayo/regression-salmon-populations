# PNW Salmon Population Analysis

### Updated group project from STAT 3400

## Goal: Using regression analysis to identify key predictors on the declining salmon population in the Northwest.
## Results: This script sets up to examine Northwest salmon populations as a whole and allows for smaller scale analysis on individual rivers. Overall, dams in the rivers have a significant affect on salmon populations as well as fish consumption.
## Next Steps: More analysis and data collection/aggregation is needed to look closer at individual rivers and their specific dam systems.

## Data Tidying & Preparation
This project brings together salmon population data with hydrology, water quality, rainfall, logging, and fish consumption datasets. Because each source uses different formats and naming conventions, a focused tidying pipeline is used to produce one consistent, analysis-ready dataset.

1. Standardizing River Names
Different datasets label the same river differently (e.g., “Umatilla” vs. “Umatilla River”).
All river names are harmonized to a single naming system before merging to prevent unmatched rows.

2. Cleaning Numeric Fields
Several datasets store numbers as character strings due to commas, units, or special reporting codes.
All numeric predictors are cleaned and converted using regex-based stripping, ensuring proper numeric typing across datasets.

3. Aggregating Water Quality Data
Water quality records come as irregular, high-frequency measurements. These are grouped by Location × Year and summarized into annual means and seasonal metrics (e.g., summer temperature averages).

4. Streamflow Summaries
Monthly Columbia River discharge values are converted into annual indicators (max flow, min flow, winter flow variability) to align with salmon time series.

5. Progressive Left-Joins
Each cleaned dataset is merged step-by-step using consistent join keys:
Basin-wide metrics by Year
Water-quality metrics by Location × Year
This produces a unified merged_data table containing all environmental and anthropogenic predictors.

6. Managing Missing Data
Legacy years often lack water-quality measurements. These missing values are retained and handled during modeling rather than during tidying, preserving the full temporal range of salmon observations.
