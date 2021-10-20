![Header Image](https://github.com/allisongao4015/oath_cases/blob/main/Images/judge-gavel-and-law-books.jpg)
Source: [Burst](https://burst.shopify.com/photos/judge-gavel-and-law-books?q=court)

# Predicting Fee Collection Outcome for Low-Level Civil Tickets Issued in New York City

## October 2021

Allison Gao

## General Overview and Issue Understanding
This analysis used data on low-level civil tickets issued by public agencies in New York City to predict fine collection outcome. This is a binary problem where a ticket either did or did not result in fine collected. 

The purpose of the analysis is to create a classification model that predicts whether or not an ticket will result in fine collection. When a ticket is issued to an individual or a commerical entity, the outcome falls into one of the four categories: 
               1) ticket is written off before a hearing takes place
               2) case dismissed
               3) guilty
               4) default, commonly known as no action by the respondent, which results in forwarding the case to the Department of Finance for fine collection. 
               
As mentioned, the third and fourth outcome lead to fine collection while the first and the second outcome do not. 

According to a study published in the Yale Law Journal, just slightly more than half of the tickets adjudicated at OATH result in fine collection. This raises serious policy implications. 

1. If the City of New York include fine collection in its budget calculation, an incorrect estimate can lead to problematic budget analysis. Therefore, this project seeks to produce a model that accurately predicts a ticket's outcome with respect to fine collection. 

2. If fine collection serves to deter violations, such a signficant number of tickets ending up in no fine collection raises serious questions about the purpose of issuing these tickets. As such, this project also aims to highlight features relevant to target outcome. 

Findings from this project is applicable to a range of stakeholders. This include the City of New York, elected officials as well as consulting firms seeking to enhance the City's fine collection policy. 


## Data 

###### Data Source
This project utilized a dataset from [Open NYC Data](https://data.cityofnewyork.us/City-Government/OATH-Hearings-Division-Case-Status/jz4z-kudi) that tracks civil tickets filed and adjudicated through the City’s independent civil court, known as the Office of Administrative Trials and Hearings (OATH). 

The dataset provides information on, among many other things, decision outcome, fine imposed, infraction charged, violation location, and respondent's address.

###### Data Shape
The entire raw dataset contained 17.8 millions rows and 78 columns. The dataset grows by the day as it is updated on a daily basis. Each row represents a ticket while each column specifies a feature, such as the ones mentioned above. 

For the purpose of this analysis, only tickest issued by the New York City Police Department and the New York City Department of Sanitation (Police Enforcement Unit) are considered. Both agencies issue low-level quality of life violations. This resulted in 766394 rows and 78 columns for this project.

###### Data Preparation
The cleaned dataset used for modeling contained 213243 rows and 271 columns (the 271 include dummy variables). To arrive at such numbers the following steps were taken:

1. Dropped all the columns that only contained null values
2. Drop all rows that did not contain information on the ticket outcome. This is important since ticket outcome is the predictive class. 
3. Additional columns were created as an effort to make the dataset more meaningful. This included appending neighborhood level income data zip codes that match up with zipcodes written on the ticket.

For the predcitive class, approximately 60% of the tickets from the cleaned dataset resulted in no fee collection while the rest did. 

![image-1](https://github.com/allisongao4015/oath_cases/blob/main/Images/target%20distribution.png) <br />


## Data Analysis 

This project used a dummy classifier (baseline model), logistic regression, decision tree, random forest, and XGBoost for machine learning modeling. Data was split into training and testing/holdout sets with cross validation done on the training set for model evaluation. Two metrics are used to evaluate model performance, and they are accuracy and precision. Increasing the precision score is the focal point of the model iteration process. 

The goal is to minimize predicting tickets that will result in fine collection when in actuality they do not. This will result in the City overestimating fine collection for budget analysis purposes. 

On the other hand, predicting that a ticket will not result in fine when in actuality it will is not as serious of an issue for the City. At the end, that's more money that the government did not account for. 

## Results 

Currently, the model that produces the highest precision score is XGBoost. It results in a 66% accuracy score and 60% in precision. As seen on the confusion matrix below (which is normalized to show precision), it is better at predicting the negative class relative to the positive . 

![image-1](https://github.com/allisongao4015/oath_cases/blob/main/Images/10:20:2021%20MVP%20Submission%20XGBoost%20Result.png) <br />


Important features were identifed from the same model. 

![image-1](https://github.com/allisongao4015/oath_cases/blob/main/Images/10:20:2021%20MVP%20Submission%20XGBoost%20Result2.png) <br />

These following features are highlighted: 

1. Class 10 of the New York City Administrative Code
2. Staten Island as the location where the ticket was issued
3. Police Department as the issuing agency
4. Class 151 of the Health Code
5. Class 56 of the RCNY rule 


## Conclusion

[this is left empty for now]
    

## Next Steps

1. Expand the dataset to include other agencies such as Department of Buildings 

2. Feature enginner the infraction charged column to be theme-based violation such as "open container", "littering", "unlicensed vendor", etc. 

3. Obtain additional census data to expand neighborhood level information 


## Additional Information

See the full analysis in the [Jupyter Notebook](https://github.com/allisongao4015/oath_cases).

For additional info, contact

Allison Gao: allison.gao@nyu.edu

## Project Structure 

```## Project Structure


├── Images    <-- visualizations generated from working notebooks and external images
├── 1st Notebook.  <-- working through the raw data
├── 2nd Notebook.  <-- EDA and feature engineering
├── 3rd Notebook.   <-- modeling 
├── Final Notebook.ipynb    <-- Jupyter Notebook containing codes detailing project's analysis 
├── Non-technical Presentation.pdf   <-- non-technical presentation slides
└── README.md
