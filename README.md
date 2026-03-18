## skagit-bay-blooms

Project Title: Examining the relationship between river discharge events and annual variability of chlorphyll concentrations in Skagit Bay, Puget Sound.

Members: Sasha Bugbee, Gaurav Jain

INTRODUCTION:
High nutrient loadings from rivers flow into Skagit Basin and disperse throughout the basin, creating algae blooms and affecting water quality. We will be comparing over four years of data to examine the influence of discharge on nutrient transport in Whidbey Basin. We will be observing the spatial mapping of NDCI over the Skagit Bay, analyzing the correlation between the indexes and discharge into the basin.

METHODOLOGY/ANALYSIS:
We plan to examine two things: (1) the effectiveness of using Sentinel-2 satellite imagery for detecting blooms and (2) the relationship between river discharge into the basin and chlorophyll concentrations for different time periods. 

The river discharge analysis and NDCI comparision is walked through in the gaurav workspace notebook. This notebook goes through pulling in USGS gauge data and identifying high flow events for Skagit River, a tributary of Skagit Bay. To relate the NDCI to river discharge, the timeseries obtained from the NDCI_processing.ipynb is used and plotted against river discharge, and a correlation coefficient is calculated.

The bloom detection is walked through in two notebooks: NDCI_exploration.ipynb and NDCI_processing.ipynb. The exploration notebook walks through how to access the data, create a mask GeoDataFrame for just the water in our focus area, filter the RGB imagery for high cloud coverage, and calculate and plot the NDCI index. The NDCI_processing.ipynb streamlines this analysis and makes it scalable through a function that can be applied to any location. Listed below are the general steps for this process:
1. pystac_client & planetary_computer → Sentinel-2 data → B02, B03, B04, B05, SCL
2. B04 + B03 + B02 → RGB → filter out images with over 30% cloud cover
3. rio.clip → create water dataset that excludes land for NDCI calculations
4. (B05 - B04) / (B05 + B04) → NDCI
5. Create get_ndci_timeseries function that creates a NDCI timeseries for any given start and end date 

HYPOTHESIS:
We will see a positive correlation between high river discharge and high NDCI. We expect a year with high river discharge to carry in more nutrients, which will fuel a larger phytoplankton bloom.

DATASETS:
- Sentinel-2-l2a
- eric.clst.org
- Esri.WorldImagery
- Skagit River https://waterservices.usgs.gov/nwis/dv/?format=rdb&sites=12200500&startDT=2022-01-27&endDT=2025-12-27&parameterCd=00060
- Stillaguamish River https://waterservices.usgs.gov/nwis/dv/?format=rdb&sites=12167000&startDT=2022-01-27&endDT=2025-12-27&parameterCd=00060

TOOLS/PACKAGES:
- pystac_client
- rioxarray
- planetary_computer
- shapely.geometry: box
- geopandas
- matplotlib.pyplot
- contextily
- odc.stac
- pandas
- matplotlib.dates
- time

RESULTS/CONCLUSION:
There is a negative correlation between discharge and NDCI. This could potentially be due to increase in mixing with more energetic flows, which is commonly observed in other systems.

Limitations of these analyses:
- The study was done during years with relatively similar peak flows
- Cloud cover issues remove a lot of satellite imagery
- Without water quality data to compare to, it is hard to evaluate NDCI efficacy
- Since the largest of the peak flows over the examination period happened this past winter, we do not get to see that influence on NDCI

Next possible steps:
- Compare LiveOcean numerical model output to NDCI 
- Explore other basins to see if there are similar findings
- Try this analysis in a basin with water quality data to expand analysis

REFERENCES:
- https://www.skagitcounty.net/EnvisionSkagit/Documents/ClimateChange/ch1_basin_overview.pdf 
- Caballero et. al. New capabilities of Sentinel-2A/B satellites combined with in situ data for monitoring small harmful algal blooms in complex coastal waters. https://www.nature.com/articles/s41598-020-65600-1
- https://apps.ecology.wa.gov/publications/documents/0203059.pdf
- Wang, M., Bodirsky, B. L., Rijneveld, R., Beier, F., Bak, M. P., Batool, M., Droppers, B., Popp, A., van Vliet, M. T. H., & Strokal, M. (2024). A triple increase in global river basins with water scarcity due to future pollution. Nature Communications, 15(1), 880. https://doi.org/10.1038/s41467-024-44947-3
