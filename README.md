![Header Image](https://github.com/allisongao4015/oath_cases/blob/main/Images/judge-gavel-and-law-books.jpg)
Source: [Burst](https://burst.shopify.com/photos/judge-gavel-and-law-books?q=court)

# Predicting Fine Collection Outcomes for Low-Level Civil Tickets Issued in New York City

## October 2021

Allison Gao

## General Overview and Issue Understanding
This analysis used data on low-level civil tickets issued by public agencies in New York City to predict fine collection outcomes. This is a binary problem where a ticket either did or did not result in a fine collected.

The purpose of the analysis is to create a classification model that predicts whether or not a ticket will result in fine collection. When a ticket is issued to an individual or a commercial entity, the outcome falls into one of the four categories: 

               1) ticket is written off before a hearing takes place
               2) case dismissed
               3) guilty
               4) defaulted, commonly known as no action by the respondent. 

Scenarios 3 and 4 result in fine collection while the first and the second outcome do not.


According to a study published in the [Yale Law Journal](https://www.yalelawjournal.org/forum/who-pays) , just slightly more than half of the tickets adjudicated by the City’s civil court resulted in fine collection. This raises a series of policy implications. 

1. If fine collection serves to deter bad behavior, but a significant number of tickets do not result in fine collection, then it raises questions on its intentions. As such, this project also aims to highlight features relevant to the predictive class. 

2.  Fines and fees are an income stream for the City of New York. An incorrect estimate can lead to problematic budget analysis. Therefore, this project seeks to produce a model that accurately predicts if a ticket will end up in fine collection. 

Findings from this project are applicable to a range of stakeholders. This includes the City of New York, elected officials, as well as public affairs firms seeking to evaluate the City's fine collection policy. 


## Data 

###### Data Source

Data for this project came from the New York City Office of Administrative Trials and Hearings (OATH) Case Status Tracker, which is accessible via  [Open NYC Data](https://data.cityofnewyork.us/City-Government/OATH-Hearings-Division-Case-Status/jz4z-kudi) . OATH adjudicates civil tickets issued by a wide range of public agencies. This project only looked at tickets issued by the Department of Sanitation, which has a sanitation police unit and the New York City Police Department. Both agencies issue low-level civil tickets, sometimes overlapping ones.


###### Data Shape

Each row of the dataset is a ticket and the columns are the information associated with the ticket. The entire raw dataset from Open NYC Data as of this month (October 2021) contains a record of 17.9 million tickets issued. However, after narrowing down the issuing agencies, the final dataset for analysis contains approximately ~760,000 tickets and 78 columns. For each column, the dataset provides information on, among many other things, decision outcome, fine imposed, infraction charged, violation location, and respondent's address.

###### Data Preparation
After data cleaning, the final dataset used for modeling contained 213,243 rows and 271 columns (the 271 columns include dummy variables). To arrive at such numbers the following steps were taken:

1. Dropped all the columns that only contained null values
2. Drop all rows that did not contain information on the ticket outcome. This is important since the ticket outcome is the predictive class. 
3. Additional columns were created as an effort to make the dataset more meaningful. This included appending neighborhood-level income data from the census.

Predictive Class 
60% of the tickets in the dataset ended up in no fine collected while approximately 40% did end up in fine collected. 

![image-1](https://github.com/allisongao4015/oath_cases/blob/main/Images/1predictiveclass.jpeg) <br />


## Data Analysis 

This project used a Dummy Classifier (baseline model), Logistic Regression, Decision Tree, Random Forest, and XGBoost for machine learning modeling. Grid search was used on all models, with the exception of the Dummy Classifier, to find the best parameters. Data was split into training and testing/holdout sets with cross validation done on the training set for model evaluation. 

Two metrics were used to evaluate model performance, and they are accuracy and precision. Increasing the precision score was the focal point of the model iteration process. 

Keeping the stakeholders in mind, fine collected is the positive outcome to focus on in order to accurately measure income coming from these tickets. In other words, by focusing on increasing the true positives, the model is trying to minimize false positives--predicting tickets that will result in fine collection when in actuality they do not. This will result in the City overestimating fine collection for budget analysis purposes. 

On the other hand, predicting that a ticket will not result in fine when in actuality it will (a false negative) is not as serious of an issue for the City. In the end, that's delivering more than what the government projects. 

Model Performance on Training Set. Random Forest and XGBoost are the two best performing models on the training set. 

![image-1](https://github.com/allisongao4015/oath_cases/blob/main/Images/2Model%20Performanceon%20TrainingSet.jpeg) <br />

## Results 

Since Random Forest and XGBoost produced similar scores, both models were tested on the holdout set. XGBoost produced a 64% accuracy score and 54% in precision. On the other hand, Random Forest produced a 70% accuracy score and 66% in precision. Therefore, Random Forest is the best performing model. 

As shown on the confusion matrix, when predicting the fine collected group, Random Forest can get it right 66% of the time. 

![image-1](https://github.com/allisongao4015/oath_cases/blob/main/Images/3confusionmatrixbestmodel.jpeg) <br />


The following features are highlighted to give insight into the analysis. 

For tickets issued in Queens, the share of tickets between the two outcome groups is pretty even. However, when we look at Staten Island, tickets with no fee collected significantly outweigh the fee collected. 




![image-1](https://github.com/allisongao4015/oath_cases/blob/main/Images/4violationlocation.jpeg) <br />

Of all the issuing parties on this graph, the disparity between the two outcomes for NYPD issued tickets is the greatest. We see that a lot of tickets issued by the NYPD do not end up in fines collected. 


![image-1](https://github.com/allisongao4015/oath_cases/blob/main/Images/5issuingagency.jpeg) <br />

AC stands for the Administrative Code of New York. Title 10 of the Administrative Code governs quality of life regulations such as noise, graffiti, and public drink. The ratio of fine collected to no fine collected is incredibly high. For someone who receives a ticket with a Title 10 violation, the chances of paying a fine is more likely than not. 

On the other hand, Title 20 of the Administrative, which governs regulation around general vendors, no fine collected significantly outweighs fine collected. 

![image-1](https://github.com/allisongao4015/oath_cases/blob/main/Images/6TicketOutcomeByViolation%20T.jpeg) <br />


## Takeaways

From a policy perspective, NYPD should consider reevaluating its ticket issuance approach. If fine collection is a means to deter bad behavior, but these tickets do not end up in fine collection, it raises questions about the purpose of issuing these tickets. 

From an efficiency standpoint, Staten Island is an interesting case for the city to explore. Efforts are invested in issuing these tickets and yet, many of them do not end up in fine collection. Valuable information can be drawn from a case study regarding Staten Island. 

    

## Project Next Steps

Goal: to increase the precision score. 

1. Expand the dataset to include other agencies (such as the Department of Buildings)

2. Obtain additional census data to expand on neighborhood-level information 


## Additional Information

See the full analysis in the [Jupyter Notebook](https://github.com/allisongao4015/oath_cases).

For additional info, contact

Allison Gao: allison.gao92@gmail.com

## Project Structure 

```## Project Structure


├── Images    <-- visualizations generated from working notebooks and external images
├── 1st Notebook.  <-- working notebook to clean the raw data
├── 2nd Notebook.  <-- EDA and feature engineering
├── 3rd Notebook.   <-- modeling 
├── Final Notebook.ipynb    <-- Jupyter Notebook contains all the notebooks combined; detailing project's analysis 
├── Non-technical Presentation.pdf   <-- non-technical presentation slides
└── README.md
