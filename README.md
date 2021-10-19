# oath_cases



General overview of the problem

New York City public agencies issue over thousands of civil tickets on a daily basis. If found in violation by the city's Office of Administrative Trials and Hearings(OATH), respondents will pay a municipal fine. However, not all issued tickets result in fine collection. In fact, according to a study published in the Yale Law Journal, just slightly more than half of the tickets adjudicated at OATH are collected. Many tickets are either dismissed or written off before they move to the prosecution stage, resulting in no fee collection. 

This raises serious policy implications on resource allocation: if a significant amount of tickets issued do not end up in fee collection, are these public agencies wasting their resources and time?  

This project seeks to build a binary classification model that predicts whether or not an issued ticket will end up in fee collection. Focusing only on low-level quality of life civil tickets, this project only looks at tickets issued by the New York City Police Department (NYPD) officers as well as New York City Department of Sanitation police officers


References to resources that help frame the problem with summary statistics and related work
https://www.yalelawjournal.org/forum/who-pays

Identification of potential stakeholders
Potential stakeholders include the City of New York as well as public advocates and public affairs firms seeking to reevaluate the efficacy of the fee and fine collection system in NYC. 


To evaluate my model, I will use accuracy and F1 score as my metric. I believe precision and recall are both important in my case. 

We want to minimize the false positives (predict fee collected when no fee is collected) so that the City does not overestimate the projected fee collected. 
