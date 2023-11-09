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

2. data_final: <br>
- This folder stores the final merged csv file called `wp_scored_city_articles_by_state.csv`
- Columns:
    - `state` : str - containing State name
    - `regional_division` : str - containing region as described by Census Bureau
    - `population` : int - state population
    - `article_title` : str - The name of the article/the city
    - `revision_id` : int - the revision id, unique identifier for each article
    - `article_quality` : str - the quality of the article as classified by ORES

### Code
The three primary notebooks are stored under the `code` folder. The extraction and analysis was broken up into three separate notebooks:
1. `step_one_ores_ranking.ipynb` - Calls the ORES api and Mediawiki api to extract rankings and revision ids
2. `step_two_combine_data.ipynb` - Merges ORES scores, revision ids, regional data and Census Bureau population data. Output is `data_final\wp_scored_city_articles_by_state.csv`
3. `step_three_analysis.ipynb` - Generates tables and plots to analyze the data files.

## Research Implications:
### Key Learnings
Initially, before doing this assignment I would have thought that the states or regions with the greatest population would have not only more articles for each city, but also higher quality articles due to more people being interested in contributing to the articles. I would have thought states such as California and Texas might have more articles. From my analysis both of my predictions were false. From the data we see that Vermont, North Dakota and Maine had the most number of articles per capita. In reality, California ranks 5th from the bottom in terms of articles per capita. After reflecting on this result, it seems obvious now that more sparsely populated states would have much higher articles per capita, purely because less people live there. Additionally, with regard to the distribution of high quality articles across the states, Vermont, Wyoming and South Dakota rank as the top three states with the most high quality articles per capita.

After doing this assignment, I feel a lot more confident with working with API calls and pulling data from different sources. I learned just how long it takes to call an API 20000 times and how its important to have logging and error handlign in the case where API calls fail. This was especially important here because there was extremely long runtimes.

### What biases did you expect to find in the data (before you started working with it), and why?

Before working with the data, I thought there could be numerous things that could bias the data. First, because we are pulling from English wikipedia, any sort of language trends across the state are not represented. It could be that articles we may consider high quality may not be reprentative of the region if a large proportion of the population is Spanish speaking for example. There are many other confounding biases that could be present. A couple examples are number of cities in the state and the age of states. We are looking at this data to see if regional or state trends affect the number of quality wikipedia articles, yet both of these confounding variables could be contributing to the trends we see.


### What (potential) sources of bias did you discover in the course of your data processing and analysis?

The main source of bias that I could see when analyzing this data was due to population. It appeared that states with pretty low populations had both higher coverage of both all articles and high quality articles. For example, the articles with the lowest number of articles per capita are North Carolina, Nevada, and California (minus the states without articles). I noticed that this is also true for the high quality articles. The states with the lowest high quality articles per capita are North Carolina, Virginia, Nevada, Arizona and California. These are also high population states. Even though measuring articles per capita seems like it should account for population differences it does not. The reason for this is because these highly populated cities are way more packed than other cities. So while a less populated state may have a similar number of people as a small highly populated state, the number of notable cities that have a wikipedia page remains the same. Rather than measuring articles per capita, perhaps it would be best to measure articles per number of cities or measure percentage of high quality articles out of all articles. 

### Can you think of a realistic data science research situation where using these data (to train a model, perform a hypothesis-driven research, or make business decisions) might create biased or misleading results, due to the inherent gaps and limitations of the data?

Perhaps we are in the situation where we are trying to improve the ORES algorithm by adding a feature that takes into account the region/state the article is being written about. If we included this data into this machine learning algorithm, our model may be highly biased towards classifying city articles that are in sparsely populated cities as higher quality. This would lead to misleading results because the model would be drawing assumptions based on the region where there is really another underlying factor. Perhaps in more populus states you have more people disagreeing over facts in wikipedia articles leading to lower quality articles.

### How might a researcher supplement or transform this dataset to potentially correct for the limitations/biases you observed?
To correct for the limitations one could adjust the metrics that we are using to compare regions. Instead of using population, another idea is to measure articles per number of cities or high quality articles per total number of articles.

## Additional Notes
- Classifying the quality of the articles using ORES is quite time consuming. This can be mitigated by shortening the throttle time in `ores_ranking.ipynb`. However, this may also result in ranking failures. After an initial run of about 4 hours I had ~2000 more articles to classify. When I increased the throttle time and ran it on the failed articles, I was able to obtain more rankings. It took one final iteration to rank all of the articles.


## License:
Distributed under the MIT License. See `LICENSE` for more details.
