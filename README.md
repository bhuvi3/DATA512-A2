# Bias in Data

Name: Bhuvan Malladihalli Shashidhara

Date: 12 Oct 2019

## Goal
The goal of this project is to observe the bias and reflect on the implications on the data analyses due to the bias present in data.

We use two main metrics for analysis of bias:
- *coverage*: The percentage of articles by population. If a country has a population of 10,000 people, and you found 10 articles about politicians from that country, then the percentage of articles-per-population would be 0.1%.
- *relative_quality*: The percentage of high-quality articles. If a country has 10 articles about politicians, and 2 of them are FA or GA class articles, then the percentage of high-quality articles would be 20%.

## Data sources used
We use the following data sources to analyse bias and its implications in data analyses:
- Wikipedia articles on political figures from various countries: Collected from [figshare](https://figshare.com/articles/Untitled_Item/5513449). This data is present in this repository in the name of ```page_data.csv```.
- Population data: Colected from [world population datasheet](https://www.prb.org/international/indicator/population/table) published by the Population Reference Bureau. This data is present in this repository in the name of ```WPDS_2018_data.csv```.

**Licence**: Please refer to the licences of the data sources in their respective website links provided above for most recent updates.

## Resources used
This analysis was prepared using Python 3.6.7 running in a Jupyter Notebook environment.  
Documentation for Python can be found here: https://devdocs.io/python~3.6/
Documentation for Jupyter Notebook can be found here: http://jupyter-notebook.readthedocs.io/en/latest/  

The following Python packages were used and their documentation can be found at the accompanying links:
- [csv](https://docs.python.org/3/library/csv.html)
- [json](https://docs.python.org/3/library/json.html)
- [os](https://docs.python.org/3/library/os.html)
- [pandas](https://pandas.pydata.org/)=0.24.2
- [pickle](https://docs.python.org/3/library/pickle.html)
- [requests](https://pypi.org/project/requests/2.7.0/)

#### Objective Revision Evaluation Service (ORES).
In order to get the predicted quality scores for each article in the Wikipedia dataset, we use a machine learning system called [ORES](https://www.mediawiki.org/wiki/ORES), which classifies an article to belong to one of the following categories (we consider an article to be of high quality if it belongs to either "FA" or "GA"):
- "FA" - Featured article
- "GA" - Good article
- "B" - B-class article
- "C" - C-class article
- "Start" - Start-class article
- "Stub" - Stub-class article

Use the REST API endpoint in this project to retrieve the quality classes. The documentation for this process can be found [here](https://ores.wikimedia.org/v3/#!/scoring/get_v3_scores_context_revid_model). Also, example code is present [here](https://github.com/Ironholds/data-512-a2).

## Files Created
This notebook creates 2 CSV files of data extracted and compiled as part of this analysis.
- ```wp_wpds_politicians_by_country.csv```: This is the main output csv file used for this analysis. The scehma of the table along with descriptions of the attributes are shown below.

| Column          | Description                               |
|-----------------|-------------------------------------------|
| country         | The name of the country.                  |
| article_name    | The name of article.                      |
| revision_id     | The revision id of the Wikipedia article. |
| article_quality | Article quality tag retrieved by ORES.    |
| population      | The population of the country.            |

- ```wp_wpds_countries-no_match.csv```: This table contains revision ids of Wikipedia articles for which we could not find matching countries in our population data. This table has same schema as the abovementioned table, but the field ```population``` contains NaNs. 

Also it creates the following auziliary files:
- ```ores_missed_rev_ids.txt```: The revision ids of the Wikipedia articles which for which we could not get the quality classes from ORES.
- ```cached_ores_api_call_res.pickle```: This is a local cache of the API call to ORES created to save time across multiple calls to the ORES API.

## Tables Created
The following result tables have been created to observe the summary of the above mentioned metrics.
- _Top 10 countries by coverage_: "10 highest-ranked countries in terms of number of politician articles as a proportion of country population".
- _Bottom 10 countries by coverage_: "10 lowest-ranked countries in terms of number of politician articles as a proportion of country population".
- _Top 10 countries by relative quality_: "10 highest-ranked countries in terms of the relative proportion of politician articles that are of GA and FA-quality".
- _Bottom 10 countries by relative quality_: "10 lowest-ranked countries in terms of the relative proportion of politician articles that are of GA and FA-quality".
- _Geographic regions by coverage_: "Ranking of geographic regions (in descending order) in terms of the total count of politician articles from countries in each region as a proportion of total regional population".
- _Geographic regions by coverage_: "Ranking of geographic regions (in descending order) in terms of the relative proportion of politician articles from countries in each region that are of GA and FA-quality".

## Reflections and Implications.


## License
This project code is released under MIT Licence.
