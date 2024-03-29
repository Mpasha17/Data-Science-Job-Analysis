# Data Science Salary Estimator: Project Overview 
* Created a tool that estimates data science salaries (MAE ~ $ 26K) to help data scientists negotiate their income when they get a job.
* Scraped over 1100 job descriptions from glassdoor using python and selenium at 4th September,2020
* Engineered features from the text of each job description to quantify the value companies put on python, excel, aws, and spark. 
* Optimized Linear, Lasso, and Random Forest Regressors using GridsearchCV to reach the best model. 
* Built a client facing API using flask 

## Code and Resources Used 
**Python Version:** 3.7  
**Packages:** pandas, numpy, sklearn, matplotlib, seaborn, selenium, flask, json, pickle  
**Scraper Github:** https://github.com/arapfaik/scraping-glassdoor-selenium  
**Scraper Article:** https://towardsdatascience.com/selenium-tutorial-scraping-glassdoor-com-in-10-minutes-3d0915c6d905 <br>
**YouTube Project Walk-Through:** https://www.youtube.com/playlist?list=PL2zq7klxX5ASFejJj80ob9ZAnBHdz5O1t  
**Flask Productionization:** https://towardsdatascience.com/productionize-a-machine-learning-model-with-flask-and-heroku-8201260503d2
**Project Idea:** https://www.youtube.com/channel/UCiT9RITQ9PW6BhXK0y2jaeg

## Web Scraping
Tweaked the web scraper github repo (above) to scrape 1100 job postings from glassdoor.com. With each job, we got the following: <br>
*Job title
*Salary Estimate
*Job Description
*Rating
*Company 
*Company Size
*Company Founded Date
*Type of Ownership 
*Industry
*Sector
*Revenue 

## Data Cleaning
After scraping the data, I needed to clean it up so that it was usable for our model. I made the following changes and created the following variables:<br>

*Parsed numeric data out of salary <br>
*Made columns for employer provided salary and hourly wages <br>
*Removed rows without salary <br>
*Parsed rating out of company text <br>
*Made a new column for company state <br>
*Added a column for if the job was at the company’s headquarters <br>
*Transformed founded date into age of company <br>
*Made columns for if different skills were listed in the job description:<br>
- Python  
- R
- Excel  
- AWS  
- Spark <br>
*Column for simplified job title and Seniority <br>
*Column for description length 

## EDA
I looked at the distributions of the data and the value counts for the various categorical variables. Below are a few highlights from the pivot tables. 

![word cloud](https://raw.githubusercontent.com/Shaon2221/Data-Science-Job-Analysis/master/Images/word_cloud.png "skill word cloud")
![job by title](https://raw.githubusercontent.com/Shaon2221/Data-Science-Job-Analysis/master/Images/job_by_title.png "job by title")
![DS by company size](https://raw.githubusercontent.com/Shaon2221/Data-Science-Job-Analysis/master/Images/ds_by_comp_size.png "datascientists by company size")
![Correlations](https://raw.githubusercontent.com/Shaon2221/Data-Science-Job-Analysis/master/Images/corr.png "Correlations")

## Model Building 

First, I transformed the categorical variables into dummy variables. I also split the data into train and tests sets with a test size of 30%.   

I tried three different models and evaluated them using Mean Absolute Error. I chose MAE because it is relatively easy to interpret and outliers aren’t particularly bad in for this type of model.   

I tried three different models: <br>
***Multiple Linear Regression** – Baseline for the model <br>
***Lasso Regression** – Because of the sparse data from the many categorical variables, I thought a normalized regression like lasso would be effective. <br>
***Random Forest** – Again, with the sparsity associated with the data, I thought that this would be a good fit. 

## Model performance
The Random Forest model far outperformed the other approaches on the test and validation sets. <br>
***Random Forest** : MAE =-29.61 <br>
***Linear Regression**: MAE = -26.172941<br>
***Ridge Regression**: MAE = 31.09
