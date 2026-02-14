## Whid-bey-Bloomin 

Project Title: Examining the relationship between river discharge events and seasonal variability of water quality in Whidbey Basin, Puget Sound.

Members: Sasha Bugbee, Tia Böttger, Gaurav Jain

High nutrient loadings from rivers flow into Whidbey Basin and disperse throughout the basin,  creating algae blooms and affecting water quality. We will be comparing two years of data, one with high river discharge in the spring and one with low river discharge in the spring, to examine the influence of discharge on nutrient transport in Whidbey Basin. Breaking it down into seasonal periods over the two year-long datasets, we will be observing (1) spatial mapping of residence time and (2) spatial mapping of dissolved oxygen, analyzing the correlation between the two and evaluating the algal bloom similarities between Sentinel-2 satellite data and LiveOcean output. [Gaurav add a (3) for your section]

Datasets:
- Meteorological data from NOAA https://tidesandcurrents.noaa.gov/stationhome.html?id=9447973 
- Gauge data from USGS: freshwater discharge volume 
      - Skagit: https://waterdata.usgs.gov/monitoring-location/USGS-12200500/#dataTypeId=continuous-00065-0&period=P7D&showFieldMeasurements=true 
      - Stillaguamish: https://waterdata.usgs.gov/monitoring-location/USGS-12170300/#dataTypeId=continuous-00065-0&period=P7D&showFieldMeasurements=true 
      - Snohomish: https://waterdata.usgs.gov/monitoring-location/USGS-12150800/#dataTypeId=continuous-00065-0&period=P7D&showFieldMeasurements=true 
- King County and Dept of Ecology: chlorophyll concentrations, dissolved oxygen concentrations at discrete sites with high residence times https://kingcounty.gov/en/dept/dnrp/nature-recreation/environment-ecology-conservation/science-services/puget-sound-marine-monitoring/water-topic-page/whidbey-basin-offshore 
- LiveOcean numerical model output: water residence time https://faculty.washington.edu/pmacc/LO/LiveOcean.html 
- Sentinel-2 data (https://dataspace.copernicus.eu/data-collections/copernicus-sentinel-missions/sentinel-2)  
- Landsat-8 data https://www.usgs.gov/landsat-missions/landsat-data-access
- Stilanguamish River near Arlington, WA - USGS 12167000 https://waterdata.usgs.gov/monitoring-location/USGS-12167000/#dataTypeId=continuous-00060-0&period=P365D&showFieldMeasurements=true&showMedian=true

Tools/packages: (primarily based off Lab 8 so far) (not comprehensive yet!)
- Geopandas 
- Rasterio mask
- Rioxarray
- Scipy.interpolate griddata https://docs.scipy.org/doc/scipy/tutorial/interpolate.html 
- pd df corr https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.corr.html 
- Queen contiguity (?) http://darribas.org/gds_scipy16/ipynb_md/04_esda.html 
- Statsmodels.tsa seasonal/stattools https://knowledge.dea.ga.gov.au/notebooks/How_to_guides/Detecting_seasonality/
- To find a linear trend in the flow of the river, we can use functions from scipy.stats. To get extreme points from the data, we can use the percentile function to find extremely high and low flow times in the time period.  

Planned methodology/approach:
We plan to follow the analysis methodology highlighted in Caballero et. al. for comparisons between satellite imagery with numerical model output on blooms. This entails pulling the satellite imagery and pulling out the spectral bands that indicate blooms (NDCI), and compare those findings to the distribution of blooms in Whidbey basin. This methodology will be applied to high and low discharge years to see how river inputs affect the spatial patterns of the blooms. We will also be able to examine residence times and chlorophyll patterns to see the correlation between the two.
As discussed during lab section, I will be looking at the volumetric flow of the Stillaguamish River in ft^3/s. I will look at how changes in volumetric flow affect the concentration of pollutants in the basin using an increase in algae as our indicator.

Expected outcomes: We will see a positive spatial correlation between increase in nutrient concentrations and increase in chlorophyll concentrations in those areas. We expect a year with high river discharge to carry in more nutrients, which will fuel a larger phytoplankton bloom.
The expected outcome is an increase in volumetric flow in the river will cause an increase in pollutant concentration in the basin, which will cause a larger algae bloom. We can analyze the pattern and calculate the max. and min. total in a given year of flow of river. We can also look at how much time it takes for a rise in the volumetric flow of the river to actually cause algae blooms in the basin. We can actually assign an increase in pollutants to industries, dumping grounds, etc. 

References:
Caballero et. al. New capabilities of Sentinel-2A/B satellites combined with in situ data for monitoring small harmful algal blooms in complex coastal waters. https://www.nature.com/articles/s41598-020-65600-1 
Wang, M., Bodirsky, B. L., Rijneveld, R., Beier, F., Bak, M. P., Batool, M., Droppers, B., Popp, A., van Vliet, M. T. H., & Strokal, M. (2024). A triple increase in global river basins with water scarcity due to future pollution. Nature Communications, 15(1), 880. https://doi.org/10.1038/s41467-024-44947-3
