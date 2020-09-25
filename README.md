# Time-Series-Modeling
Here we utilize a SARIMAX time series model to discover the top 5 zip codes of Los Angeles, California to invest in. 

### Author: Jessica Forrest-Baldini

## Business Case

A real estate investment group is looking to invest in single family homes in Los Angeles and wants to know the top 5 best zip codes to invest in for the greatest ROI (return on investment) with the least amount of risk.

The strategy is buy and hold, so we will be looking at 5 year projections. And for further work we recommend analyzing the rental markets for the top 10 zip codes for comparison. 

## Data

From Zillow
https://www.zillow.com/research/data/

Zip_zhvi_uc_sfr_tier_0.33_0.67_sm_sa_mon.csv

Filename changed to: up_to_date_zillow_data.csv in this repository

## Contents 

- figures - Figures folder
- .gitignore - Git ignore file
- README.md - Readme file
- los_angeles_real_estate_notebook.ipynb - Notebook
- up_to_date_zillow_data.csv - Data

## Methods 

**Data & Model**

The data used were for single family homes on Zillow from 1/31/1996 through 7/31/2020 (the most current data available at the time of this project).

These were median home values for the 33rd - 67th percentile of each region. The data were seasonaly smoothed by Zillow, however upon decomposition, seasonality was discovered, so a SARIMAX model was used to account for seasonality.

**Parameter Selection**

A gridsearch was conducted to find the optimal parameter values for the SARIMAX model. I averaged all Los Angeles zip codes and optimized parameters by lowest BIC. However, when I then applied this model to zip codes individually, the forecasted home values were off the charts high with very large confidence intervals. 

I then ran a gridsearch for one zip code, West Hollywood and applied the model with those optimized parameters to all 100 zip codes, also considering RMSE (if RMSE was lower for a slightly higher BIC, then the lower RMSE set of parameters would be used). This yielded clear results with a clear trend and projections that had much smaller confidence intervals than the all-of-LA-averaged model. 

## Results

### Top 10 Zip Codes & Metrics  

!["Top 10 Zip Codes"](figures/top_10_table.csv)

### Feature Importance

The top 3 most important features were the same for Random Forest and XGBoost, and those were:

  #1: Having an international plan 
  #2: Total charges
  #3: Customer service calls (# of)
  
!["Feature Importance"](figures/feat_rank_XGB.png)
  
### EDA Insights

We found that:

- Customers with international plans are more likely to churn, and that customers with international plans appeared to have slightly higher charges.
- Customers who had made more customer service calls were more likely to churn.
- When it came to charges there were two distinct modes of churners: those with significantly higher charges than non-churners, and those with lower charges than non-churners.

!["International Plan"](figures/international%20plan.png)
!["Customer Service Calls"](figures/customer%20service%20calls.png)
!["Total Charges"](figures/total%20charges.png)


## Recommendations

I recommend using XGBoost as it performs faster and has a clear pattern of feature importance, and also has comparable recall and fewer false positives (thus slightly higher accuracy) than Random Forest.

### Business

There are a few different groups that I want to make recommendations for. It seems we have 3 groups of churners:

- Those on an international plan
- Those with high charges
- Those who have made a high number of customer service calls

###  International Plan

Those with an international plan that churned had slightly higher charges. In future work I would want to find out exactly why people on international plans are churning. It could be that competitors have better plans or it could be that they moved back to another country. Are these customers traveling for work or here in the states temporarily? Do competitors have much more attractive and perhaps more cost effective international plans?

###  High Charges

This group is probably being lost to competitors. I would recommend looking at competitors plans. Do these customers go over their plan? If so I would recommend proactively offering a higher grade package to this customer group to save them money instead of them having high overage charges.

An alternative might be some type of booster package. Where if a customer goes over, they're given an add on package at a better rate than their overage, but still higher than their plan rate.

I would also recommend proactively letting these customers know when they're nearing an overage and offering them a plan that better fits their usage needs to prevent overages and thus high charges.

###  High Customer Service Calls

I know telecommunications companies have a special department for customers who want to cancel. They offer them more competitive plans, savings or offers. It would be good to train customer service representatives to make better offers early on. I understand there may be a tradeoff here between making the offer to more customers who may not churn and thus finding a balance between proactively retaining customers who might churn and making better offers to customers who may not churn would be important.

There wasn't an apparent relationship between total charges and customer service calls. However, charges of churners were bi-modal, so these could be averaging each other out. I will speak on this in the future work section.

I recommend the department that deals with cancellations proactively contact customers who have made more than 5 customer service calls as it seems that's where churn rate starts to significantly increase.

## Further Research

For future work I would recommend exploring the customer service calls of churners who made a high number of customer service calls.

I would also recommend researching more competitive plans that exist, especially for high usage and international plans.

As far as data science work, I would like to sus out the two groups of charges that churn (lower and higher) and discover why the lower group is churning and if there is any clear pattern there.

## Thank you!

For any additional questions, please feel free to connect with me at jlforrestbaldini@gmail.com or on LinkedIn at https://www.linkedin.com/in/jessica-forrest-baldini-0468111a4/
