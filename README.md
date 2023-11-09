# us-wildfire-analysis
## Common Analysis Project - Part One

## Project Goal
- Part 1 - Common Analysis sets the stage for the subsequent assignments. In Part 1 you conduct a base analysis. All of the students in the class will conduct the same analysis, but with a slightly different data subset.
- Part 2 - Extension Plan will require you to ask a human centered data science question that extends the work in Course Project Part 1 - Common Analysis. 
- Part 3 - Presentation will require you to give a modified (shorter) PechaKucha presentation of your completed project.
- Part 4 - Project Repository, creation of a fully documented repository and also requires the submission of a written project report.


## Data Sources
1. Combined wildland fire datasets for the United States and certain territories: https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81
     - *note:* This file must be downloaded and unzipped into the data_raw folder 
3. US EPA Air Quality System API: [https://aqs.epa/data/api](https://aqs.epa.gov/aqsweb/documents/data_api.html)

## Contents:
### Data folders
1. data_raw: <br>
The data raw folder contains the raw data files as extracted from the data sources. It consists of three main files and an additional supplementary file.
    1. `Wildfire Cities Assignments.xlsx` - The city assignments for this project
    2. GeoJSON Exports folder - this is the exported folder from data source 1. It is far to large to upload to github.

2. data_intermediate: <br>
The data_intermediate folder contains intermediary csv files that were used in the process of creating the visualizations.
   1. avg_aqi_per_year.csv - contains the aggregated aqi per year from the EPA api
   2. distances.csv - a csv file containing the distances for each of the fires in from the Combined Wildfire dataset.
   3. smoke_estimate.csv - a csv file that contains the smoke estimates computed based on the Combined Wildfire dataset in data source 1

### Code
The three primary notebooks are stored under the `notebooks` folder. The extraction and analysis was broken up into three separate notebooks:
1. `analysis.ipynb` - Contains the main code for generating visualizations and performing statistical modeling
2. `get_aqi_data.ipynb` - Calls the EPA api to extract AQI
3. `get_smoke_estimate.ipynb` - Loads in data source 1 and generates the smoke estimate

## Additional Notes
- Many of the large files were not uploaded due to GitHub limits. They will be uploaded later.


## License:
Distributed under the MIT License. See `LICENSE` for more details.
