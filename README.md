# Are U.S. Climate Disasters Accelerating?

A statistical analysis of NOAA's billion-dollar weather and climate disasters in the United States from 1980 to 2024.

**[View Live Dashboard on Tableau Public]([https://public.tableau.com/app/profile/thomas.kirvin/viz/Book2_17794238190500/Dashboard1?publish=yes])**

![Dashboard Screenshot](tableau/dashboard_screenshot.png)

## Question

Is the United States experiencing more frequent and more costly climate-related disasters over time, and is that trend statistically meaningful or just noise?

## Key Findings

- **403 billion-dollar disasters** occurred in the U.S. between 1980 and 2024, causing **$2.917 trillion** in CPI-adjusted damages.
- The 2020s have averaged **6.97x more disasters per year** than the 1980s (23.0 vs. 3.3 events per year).
- The increase in annual event count over time is highly statistically significant (**p < 0.0001**), confirmed by both a linear regression and a non-parametric Mann-Kendall trend test.
- **Tropical cyclones drive the majority of damage**, accounting for 52.89% of total CPI-adjusted costs, followed by severe storms (17.62%) and droughts (12.61%).
- Disaster costs as a share of GDP show a weaker upward trend than event counts, suggesting growth in event frequency outpaces growth in per-event economic impact relative to the broader economy.

## Data

- **Disaster data:** [NOAA NCEI Billion-Dollar Weather and Climate Disasters](https://www.ncei.noaa.gov/access/billions/), 1980–2024
- **GDP data:** Real GDP, retrieved from [FRED (Federal Reserve Economic Data)](https://fred.stlouisfed.org/)
- **Cost adjustments:** Disaster costs are CPI-adjusted to 2024 USD (NOAA's base year). Real GDP is in chained 2017 USD (BEA's base year). The trend significance results are robust to base-year harmonization.

## Methodology

Annual disaster counts and CPI-adjusted costs were aggregated from the NOAA dataset and joined with FRED GDP data to compute disaster cost as a percentage of GDP for each year. Decade-level averages were calculated to enable comparison across eras.

Two statistical tests were applied to the annual event count series (1980–2024):
1. **Linear regression** of event count against year (parametric)
2. **Mann-Kendall trend test** (non-parametric)

Both returned p-values below 0.0001, providing strong evidence that the increase in billion-dollar disasters over time is not attributable to random variation.

Cost share by disaster type was computed as each category's percentage of total CPI-adjusted damages across the full 1980–2024 period.

## Caveats

- **The 2020s decade reflects only 5 years of data (2020–2024)**, not a full decade. The events-per-year comparison in the KPIs normalizes for this, but the raw decade bar should be interpreted with the partial-decade context in mind.
- **The "billion-dollar" threshold is itself sensitive to inflation.** As prices rise, more events cross the threshold, which may inflate event-count trends. CPI adjustment of cost data helps separate this effect, but event count itself is unadjusted for threshold creep.
- **Base-year mismatch between datasets:** Disaster costs are in 2024 USD while GDP is in 2017 USD. This affects the absolute level of the cost-as-share-of-GDP metric but does not change the direction or significance of the trend.
- **Exposure growth is not controlled for.** Increases in population, infrastructure value, and coastal development over the study period contribute to disaster costs independently of climate factors.

## Tools

- **Python:** pandas, numpy, scipy.stats (linregress, F-distribution), pymannkendall, scikit-learn, matplotlib
- **Tableau Public** for dashboard development and publication
- **Statistical methods:** linear regression, Mann-Kendall trend test, decade aggregation, share-of-total calculations

