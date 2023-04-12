# Data Science Job Market Analysis

This repository serves as a complete analysis of the Data Science Job Market as of March 2023, as a prospective salary
indicator and skills checklists for students graduating from the Bachelor of Advanced Computing Sciences (DACS) at 
Maastricht University, the Netherlands. 
****
Key research questions of the analysis include: 
1. What is the expected salary of a graduating DACS student in the current job market? 
2. What are skills in high demand in the current job market
3. How has DACS prepared students to enter the job market, in terms of in demand skills. 

### Findings

![Geographic Distribution](resources/geo_distribution.png)

Predominantly European and US jobs were scraped and gathered. Smaller hotspots include: Dubai, South Africa, 
Singapore, and Canada.  For a full list of scraped countries please review [collection.ipynb](collection.ipynb)

![Geo Salary Availability (incl. US)](resources/geo_salary_incl_us.png)

However, not all scraped job postings contained salary information, as countries have varied specifications 
regarding salary transparency. 

![Geo Salary Availability (excl. US)](resources/geo_salary_excl_us.png)

Removing the US for a clearer image of the salary transparency of remainder of the job postings. 
It must be noted that **Anywhere** is remote working, and it has become the second-largest source of salary transparent 
job listings scraped. 

![In Demand Skills](resources/skills.png)

From the job listings with available salary information, the required skills/ tools were extracted,
forming the skill/ tool demand visualization. Python, Machine Learning, and SQL being the top three requirements 
for any prospective data science position. 

![Salary Ranges](resources/salary_ranges.png)

Each country's salary ranges were converted into Euro's as a base country providing direct comparisons. 
It must be noted that these ranges include all Data Science job positions from Junior Data Scientists, 
Senior Data Scientist, and Data Scientist project managers. 
It is worthwhile noting that **Anywhere** or remote Data Science Positions have the second highest media salary value

![Model Residuals](resources/model_residuals.png)

Three models were trained to generate an estimate salary from a set of skills/ tools:
1. LassoCV Regression model
2. Decision Tree
3. Random Forest Model
The best performing model is the Random Forest, with a redidual of approximately 10000 Euros in its predictions. 

For further information on the above visualizations and more indepth explanations, please review [eda.ipynb](eda.ipynb)


## Project Structure
### Data Collection
The data collection makes use of [SerpAPI](https://serpapi.com/), a freely accessible web-scraping tool, allowing 
scraping of multiple search engines including Google. This was utilized to target Google Job listings in order to gather 
current Data Science job offerings.

The Jupyter Notebook performing data extraction is `collection.ipynb`
The collected data is stored in `data.csv`.

### Data Cleaning 
The scraped Google job listings are returned in an unstructured format. Multiple cleaning processes are required in order 
to generate meaningful data, ranging from NLP Question and Answer models, skill keyword extraction, and dealing with 
outliers, missing values, etc. 

The Jupyter Notebook performing the data cleaning is `pipeline.ipynb`. 
The cleaned data is stored in `data_clean.csv`.

Note: At each stage of the data cleaning, the data is stored in order to avoid repeated computation. 
These interim stores include: `data_cache/data_salaries.csv`, `data_cache/data_countries.csv`, `data_cache/data_country.csv`, `data_salaries`.

### EDA and Modelling
The data was explored further using EDA techniques and prepared for modelling purposes. 
Three models were utilized, a standard Linear Regression model using Lasso Regularization, 
a Decision Tree Regression Model, and a Random Forest Regression Model. 

The Jupyter Notebook performing the EDA and Modelling is `eda.ipynb`. 

### Notes and Proptypes
This directory contains initial attempts at the now final processes includes in the steps above. 

## Video Demonstration
This video provides a short 2-minute overview of the completed analysis and discoveries. \
Link: https://youtu.be/72cyQKITGjs 



## Project Setup
### Conda
Setup conda environment from file:
```
conda env create -f data_madness_env.yml
```

and then activate the environment as ususal:
```
conda activate data_madness
```

Before pushing code, if you have made changes to the environment, run the following:
```
conda env export > data_madness_env.yml
```

### Troubleshooting

#### 1. GoogleSearch import fails with conda environment

If an error occurs in
```
from serpapi import GoogleSearch
```

run
```
pip install google-search-results
```
