# US Data Center Capacity Growth & Spatial Analysis

A group analytics project examining how US data center power capacity is growing over time and where it is concentrating geographically. The analysis uses a real-world sample dataset obtained from Aterio (300 facilities, 64 fields, including coordinates, power capacity, and activation timelines).

## Research Questions

- When is capacity growing fastest?
- Where are new facilities clustering?
- Who is most exposed to the resulting infrastructure/grid stress?

## Key Findings

### Clustering (K-means, K = 5)
After cleaning the dataset down to 231 facilities and 9 usable numeric features, five facility archetypes emerged:

- **Cluster 0 - Mid-size Southwest 2020s**: medium facility and power (~16-24 MW), in the south-west, built around 2020.
- **Cluster 1 - Large New Plains Hubs**: big sites (~380k sqft, ~60-66 MW) in the central plains, very recent activation (~2024+).
- **Cluster 2 - Upper-Midwest High-Power 2024**: medium-large facilities (~270k sqft, ~46-55 MW), more to the east/upper-Midwest, also very new (~2025).
- **Cluster 3 - Small Legacy Sites**: smaller, low-power data centers (~105k sqft, ~11-12 MW) around the Ohio/Indiana region, clearly older (~2009).
- **Cluster 4 - Hyperscale Mega-Campuses**: very large campuses (~600k+ sqft, ~100-115 MW), also in the Midwest corridor, relatively modern (~2020).

K = 5 was chosen as a balance between the elbow-curve inertia and the silhouette score.

### Linear Regression / "Hyperscale Shock"
Historical data shows a steady climb of roughly 53 MW/year in added capacity, projecting modestly to about 858 MW by 2028. However, actual 2026-2027 project filings are running three to four times higher than that forecast, pointing to an AI-driven demand spike that historical trend lines do not capture.

### Spatial Modeling
Adding location (via a KNN approach) to the regression improved explanatory power substantially, confirming that both timing and geography matter for where capacity lands. Power capacity is heavily concentrated in a handful of states, led by Texas, Virginia, Arizona, and Illinois.

## Repository Structure

- `data/data_center_inventory_sample_sep_2025_with_Balancing_Authorities.csv` - the 300-row sample dataset
- `Linear Regression_Akash.R` - data cleaning, annual trend aggregation, regression forecast, and visualization
- `spatial_analysis.R` - state-level choropleth mapping of total power capacity
- `spatial_model.rmd` - exploratory spatial data setup (in progress)

## Requirements

R with the following packages: tidyverse, lubridate, scales, sf, maps, ggplot2, tigris, spdep

## Known Limitations

- Small sample size (300 facilities before cleaning)
- `spatial_analysis.R` references a `data/State_data.csv` file that is not currently present in the repo
- The R Markdown spatial model file is incomplete
- `Clustering` and `K-means_Arthur` are placeholder files left over from early project setup
