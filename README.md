# us-wildfire-analysis
# Wildfire Impact on Montana's Economic Stability

## Overview

This research project delves into the profound implications of wildfires on the economic stability of Montana. The primary focus revolves around the overarching question: "How do wildfires impact the economic stability of Montana?" To address this, the study explores specific sub-questions to gain comprehensive insights into the intricate relationships between wildfire-related factors and Montana's GDP.

## Research Questions

1. **Correlation Analysis:** The project investigates the existence of a robust linear correlation between key factors influenced by wildfires—namely, smoke, air quality, and national park visitation—and the GDP of private industries linked to national parks in Montana.

2. **Time Series Forecasting:** The study extends its exploration to historical trends, aiming to uncover insights into the past trajectories of variables like smoke, air quality, and national park visitation. By doing so, it seeks to project valuable foresights into the future trajectory of Montana's GDP.

## Methodology

The methodology involves a multifaceted approach, including correlation analysis, time series forecasting, and advanced statistical techniques. Various data sources, such as air quality indices, park visitation records, and GDP measurements, are harnessed to unravel the intricate dynamics influenced by wildfires.

## Importance of Findings

Understanding the impact of wildfires on Montana's economic landscape is crucial for informed decision-making and policy formulation. By exploring correlations and historical trends, this research project aims to provide actionable insights for city officials, policymakers, and residents to navigate and mitigate the economic consequences of wildfires. The findings contribute not only to the academic discourse but also serve as a practical guide for those tasked with safeguarding Montana's economic well-being.



## Data Sources
1. **Combined Wildland Fire Datasets**
   - **Data Source:** USGS ScienceBase-Catalog, FRESC Public Data
   - **License:** Public Domain
   - **Link:** [USGS ScienceBase-Catalog](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81)
   - **Description:** Collection of US wildfire data records, encompassing features such as USGS ID, fire type, year of occurrence, acres burned, and geographic information representing wildfire location and size.

2. **AQI Dataset**
   - **Data Source:** US EPA Air Quality System API
   - **License:** Public Domain
   - **Link:** [US EPA Air Quality System API](https://aqs.epa/data/api)
   - **Description:** EPA's API providing daily measurements of pollutants (e.g., O2, SO2, NO2) from specific monitoring stations.

3. **Annual Visitation and Record Year by Park (1904 - Last Calendar Year)**
   - **Data Source:** IRMA National Park Service Visitor Use Statistics
   - **License:** Public Domain
   - **Link:** [STATS - National Reports (nps.gov)](nps.gov)
   - **Description:** NPS Integrated Resource Management portal for downloading datasets of temporal visitation estimates from any US national park. Specific subset for Montana includes parks like Glacier National Park, Yellowstone National Park, etc.

   **Method:**
   - Select Annual Visitation and Record by Park (1904 - Last Calendar Year)
   - Generate a report using all regions and park types.
   - Limit parks to a subset of national parks in Montana.
   - Download the report as a CSV file.

4. **GDP Data**
   - **Data Source:** Bureau of Economic Analysis - US Department of Commerce
   - **License:** Public Domain
   - **Link:** [BEA: Regional Economic Accounts](https://www.bea.gov/itable/iTable.cfm?ReqID=70&step=1#reqid=70&step=1&isuri=1)
   - **Description:** BEA provides GDP estimates for all US states, covering private and government sectors. The downloaded tables include FIPS code, state name, region, tablename, linecode, industry classification, description, unit, and yearly recorded GDP.

   **Method:**
   - Navigate to Gross Domestic Product by State.
   - Download the required files, e.g., March 31, 2023 (Gross Domestic Product by State, 4th Quarter and Annual 2022) and Annual GDP by State and Industry.
## Contents:
### Data folders
1. data_raw: <br>
The data raw folder contains the raw data files as extracted from the data sources. It consists of three main files and an additional supplementary file.
    1. `Wildfire Cities Assignments.xlsx` - The city assignments for this project
    2. GeoJSON Exports folder - this is the exported folder from data source 1. It is far to large to upload to github.
    3. `SAGDP2N_MT_1997_2022.csv` - Montana GDP data from the IRMA NPS contains columns such as FIPS, GeoName, Region, TableName, LineCode, IndustryClassification, Description, Unit, 1997, 1998....2022
    4. `SAGDP2S_MT_1963_1997.csv` - Historical Montana GDP data from the IRMA NPS contains columns such as FIPS, GeoName, Region, TableName, LineCode, IndustryClassification, Description, Unit, 1997, 1998....2022
    5. `SAGDP2N_WA_1997_2022.csv` - Washington GDP data from the IRMA NPS contains columns such as FIPS, GeoName, Region, TableName, LineCode, IndustryClassification, Description, Unit, 1997, 1998....2022
    6. `SAGDP2N_CA_1997_2022.csv` - California GDP data from the IRMA NPS contains columns such as FIPS, GeoName, Region, TableName, LineCode, IndustryClassification, Description, Unit, 1997, 1998....2022

2. data_intermediate: <br>
The data_intermediate folder contains intermediary csv files that were used in the process of creating the visualizations.
   1. `montana_aqi.csv` - contains the aggregated aqi measurements extracted using the `get_aqi_data.ipynb`. Columns year, max_aqi, avg_aqi, aqi100, and aqi75. All features are float values. See methodology from final paper for more details.
   2. `montana_gdp.csv` - contains the aggregated and cleaned gdp data from the BEA. Output of `get_gdp_data.ipynb`. Has columns year and gdp.
   3. `distances.csv` - a csv file containing the distances for each of the fires in from the Combined Wildfire dataset.
   4. `smoke_estimate.csv` - a csv file that contains the smoke estimates computed based on the Combined Wildfire dataset in data source 1. Contains two columns year (int) and smoke_estimate (float). This is the output from `get_smoke_estimate.ipynb`

### Code
The three primary notebooks are stored under the `notebooks` folder. The extraction and analysis was broken up into three separate notebooks:
1. `final_analysis.ipynb` - Contains the main code for performing the correlation analysis and time-series forecasting.
2. `get_aqi_data.ipynb` - Calls the EPA api to extract AQI and saves the output to data_intermediate
3. `get_smoke_estimate.ipynb` - Loads in data from USGS and generates the smoke estimate and saves output to data_intermediate
4. `get_gdp_data.ipynb` - Loads in the GDP data from the BEA and generates the smoke estimate and saves output to data_intermediate. 

## Additional Notes
- The USGS wildfires data was not uploaded due to GitHub limits. However, download methods provided in detail within the data sources section. 


## License:
Distributed under the MIT License. See `LICENSE` for more details.
