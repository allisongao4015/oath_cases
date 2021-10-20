![Header Image](https://github.com/allisongao4015/oath_cases/blob/main/Images/judge-gavel-and-law-books.jpg)
Source: [Burst](https://burst.shopify.com/photos/judge-gavel-and-law-books?q=court)

# Predicting Fee Collection Outcome for Low-Level Civil Tickets Issued in New York City

## October 2021

Allison Gao

## General Overview and Issue Understanding
This analysis used record on civil tickets from New York City's Office of Administrative Trials and Hearings (OATH) to predict fee collection outcome. The purpose of the analysis is to create a binary classification model that predicts whether or not an ticket will result in fine collection. When a ticket is issued to an individual or a commerical entity, the outcome falls into one of the four categories: 1) ticket is written off before a hearing takes place, 2)case dismissed,3) guilty, and 4)default, commonly known as no action by the respondent, which results in forwarding the case to the Department of Finance for fine collection. As mentioned, the first and the second outcome result in no fee collected while the last two do lead to fine collection. 

According to a study published in the Yale Law Journal, just slightly more than half of the tickets adjudicated at OATH are collected. This raises serious policy implications. If the City of New York include fine collection in its budget calculation, an incorrect estimate can lead to problematic budget analysis. Therefore, this project seeks to produce a model that accurately predicts a ticket's outcome with respect to fine collection. 

## Data 

###### Data Source
This project utilized a dataset from [Open NYC Data](https://data.cityofnewyork.us/City-Government/OATH-Hearings-Division-Case-Status/jz4z-kudi) that tracks civil tickets filed and adjudicated through the City’s independent civil court. The dataset provides information about the decision outcome, fine imposed, infraction charged, violation location, respondent's address, and many other relevant information. 

###### Data Shape
The entire raw dataset contained 17.8 millions rows and 78 columns. The dataset grows by the day as it is updated on a daily basis. Each row represents a ticket while each column specifies a feature, such as the ones mentioned above. 

For the purpose of this analysis, only tickest issued by the New York City Police Department and the New York City Department of Sanitation (Police Enforcement Unit) are considered. Both agencies issue low-level quality of life violations. This resulted in 766394 rows and 78 columns for the project.

###### Data Preparation
The cleaned dataset used for modeling contained 213243 rows and 271 columns (the 271 include dummy variables). To arrive at such numbers the following steps were taken:

1. Dropped all the columns that only contained null values
2. Drop all rows that did not contain information on the ticket outcome. This is important since ticket outcome is the predictive class. 
3. Additional columns were created as an effort to make the data more meaningful. This included appending neighborhood level income data for each zip code that's    associated with a ticket. 

For the predcitive class, approximately 60% of the tickets from the cleaned dataset resulted in no fee collection while the rest did. 

(https://github.com/allisongao4015/oath_cases/blob/main/Images/target%20distribution.png)


## Data Analysis 

This project used a dummy classifier (baseline model), logistic regression, decision tree, random forest, and XGBoost for machine learning modeling. Data was split into training and testing/holdout  sets with cross validation done on the training set for model evaluation. Two metrics used to evaluate model performance are accuracy and precision. 

## Results 

Currently, the model that produces the highest precision score is (). It is good at predicting class (). 

Important features were identifed from Decision Tree and Random Forest by the value of the coefficient to highlight relevant features. 

The following features appeared in both models: 

1. Sanitation Police
2. Administrative Code 10
3. Median household income 


## Conclusion

Results from this project’s analysis suggested the following recommendations:

1.  

2. 

3. 
    

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
├── 1st Notebook
├── 2nd Notebook
├── 3rd Notebook
├── Final Notebook.ipynb    <-- Jupyter Notebook containing codes detailing project's analysis 
├── Non-technical Presentation.pdf   <-- non-technical presentation slides
└── README.md
