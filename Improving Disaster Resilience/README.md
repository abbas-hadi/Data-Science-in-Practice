# Improving Disaster Resilience

Indiana University, DSCI-D 592 Data Science in Practice, Fall 2023 (team project)

## Goal

Give local planners a way to find counties that face similar natural hazard risks and sit close by, so neighboring communities can compare notes and coordinate mitigation and recovery planning.

## Data

- **FEMA National Risk Index (county level):** composite risk, expected annual loss, social vulnerability, community resilience, and scores for 18 hazard types such as heat wave, hurricane, wildfire, riverine flooding and winter weather
- **CDC/ATSDR Social Vulnerability Index 2020:** all 3,143 US counties
- **County centroid coordinates:** latitude and longitude for each county
- **County boundaries:** GeoJSON keyed by FIPS code
- **OpenFEMA Disaster Declarations Summaries (v2):** every federal disaster declaration since 1953, pulled through the OpenFEMA API

All county datasets are joined on five-digit FIPS codes.

## Approach

1. **Risk clustering:** pick a hazard (or any set of variables), standardize the features, reduce them with PCA, and group counties with k-means.
2. **Peer county search:** for a target county, compute haversine great-circle distances to every other county and return the nearest ones in the same risk cluster.
3. **Mapping:** plot the target county and its peers on an interactive Folium map, with Plotly charts of the clusters.
4. **Forecasting:** count declarations per year by hazard type, test for stationarity, and forecast five years ahead with ARIMA.

Peer results can be exported to CSV, ranked by distance, for planners to use.

## Notebooks

| Notebook | What it does |
| --- | --- |
| `final_delivery copy.ipynb` | Final deliverable: data joins, clustering, peer county search and Folium maps |
| `fema_data_extracts.ipynb` | Paginated extraction of any OpenFEMA dataset through the API |
| `FEMA_Forecasting_Analysis.ipynb` | ARIMA forecasts of disaster declarations by hazard type (written by teammate Andrew Sommers) |
| `OpenFEMA Dataset.ipynb` | Exploration of FEMA Individuals and Households Program registrations by county |

## Example

Pick a county by FIPS code, such as 6087 (Santa Cruz County, CA), and cluster on the National Risk Index. The tool returns the 10 nearest counties with the same risk profile and maps them.

## Tools

Python, pandas, scikit-learn (StandardScaler, PCA, KMeans), statsmodels (ARIMA), Folium, Plotly, OpenFEMA API
