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
The data_intermediate folder contains intermediary csv files that were used in the process of creating the finalized data file which is stored in data_final.
    1. `us_cities_revid.csv` : This file is an intermediary output from `src\step_one_ores_ranking.ipynb`. It is the combined data from `us_cities_by_state_SEPT.2023.csv` and the revision id data pulled from the wikipedia api.
    2. `us_cities_score_failures.csv` : Temporary file used to store article names that failed in ORES api call (empty because all succeeded)
    3. `us_cities_score.csv` : unsorted raw output merged from ORES and data sources
    4. `us_cities_score_sorted.csv` : sorted output from ORES of the ~20,000 city articles.

### Code
The three primary notebooks are stored under the `notebooks` folder. The extraction and analysis was broken up into three separate notebooks:
1. `analysis.ipynb` - Contains the main code for generating visualizations and performing statistical modeling
2. `get_aqi_data.ipynb` - Calls the EPA api to extract AQI
3. `get_smoke_estimate.ipynb` - Loads in data source 1 and generates the smoke estimate

## Additional Notes
- Many of the large files were not uploaded due to GitHub limits. They will be uploaded later.


## License:
Distributed under the MIT License. See `LICENSE` for more details.
