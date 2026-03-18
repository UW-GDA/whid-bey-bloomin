## skagit-bay-blooms

Project Title: Examining the relationship between river discharge events and annual variability of chlorphyll concentrations in Skagit Bay, Washington
Members: Sasha Bugbee, Gaurav Jain, Tia Bottger (in spirit!)


INTRODUCTION:
High nutrient loadings from rivers flow into Skagit Basin and disperse throughout the basin, creating algae blooms and affecting water quality. We will be comparing over four years of data to examine the influence of discharge on nutrient transport in Whidbey Basin. We will be observing the spatial mapping of NDCI over the Skagit Bay, analyzing the correlation between the indexes and discharge into the basin.


METHODOLOGY/ANALYSIS:
We plan to examine two things: (1) the effectiveness of using Sentinel-2 satellite imagery for detecting blooms and (2) the relationship between river discharge into the basin and chlorophyll concentrations for different time periods. To detect phytoplankton via satellite imagery, NDCI (Normalized Difference Chlorophyll Index).

The river discharge analysis is walked through in Gaurav’s notebook. This notebook steps through the analysis done on the Skagit and Stillaguamish rivers' flow data and how they relate to NDCI data. Listed below are the general steps for this process:
1. Data was collected from the USGS portal for both rivers and calculated the correlation coefficient between them. Using percentile thresholding, high-flow events and months of high discharge were identified, which proved useful later in the analysis.
2. To relate the NDCI to river discharge, the median NDCI timeseries was plotted with discharge, using a different y-axis. Then the correlation coefficient was calculated for NDCI and river discharges, as well as the lag time (0-90 day limit) correlation coefficient of big flow events, big NDCI values, and average correlation.

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
There is a negative correlation between discharge and NDCI. This could be potentially due to increase in mixing with more energetic flows, which is commonly observed in other systems.
- Big flow events correlation: -0.216 → high discharge & decreased NDCI
- Big NDCI events correlation: -0.444 → large blooms & low river flow

Limitations of these analyses:
- Study done during years with similar peak flows
- Cloud cover issues
- No water quality data to validate NDCI
- No data yet on summer 2026 following the large discharge this past winter

Next possible steps:
- Compare LiveOcean numerical model output to NDCI 
- Explore other basins to see if there are similar findings
- Try this analysis in a basin with water quality data to expand analysis


REFERENCES:
- https://www.skagitcounty.net/EnvisionSkagit/Documents/ClimateChange/ch1_basin_overview.pdf  
- Caballero et. al. New capabilities of Sentinel-2A/B satellites combined with in situ data for monitoring small harmful algal blooms in complex coastal waters. - https://www.nature.com/articles/s41598-020-65600-1
- Seasonal Patterns and Controlling Factors of Primary Production in Puget Sound’s Central Basin and Possession Sound. (2002). https://apps.ecology.wa.gov/publications/documents/0203059.pdf 
- Wang, M., Bodirsky, B. L., Rijneveld, R., Beier, F., Bak, M. P., Batool, M., Droppers, B., Popp, A., van Vliet, M. T. H., & Strokal, M. (2024). A triple increase in global river basins with water scarcity due to future pollution. Nature Communications, 15(1), 880. https://doi.org/10.1038/s41467-024-44947-3 
- Xu, M., Liu, H., Beck, R., Lekki, J., Yang, B., Shu, S., Kang, E. L., Anderson, R. C., Johansen, R., Emery, E., Reif, M., & Benko, T. (2019). A spectral space partition guided ensemble method for retrieving chlorophyll-a concentration in inland waters from Sentinel-2A satellite imagery. Journal of Great Lakes Research, 45(3), 454–465. https://doi.org/10.1016/j.jglr.2018.09.002  


