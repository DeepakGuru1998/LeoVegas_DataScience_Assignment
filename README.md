# LeoVegas DataScience Assignment
This repository contains Jupyter notebooks performing different ML tasks and market analysis. 

### Data Cleaning
Various Data cleaning tasks were performed to make the quality of the data better before proceeding to the actual Machine Learning work. 

#### i. Country replacement
Sometimes the league names are misplaced under country. So, I find all the cases where the league is misplaced and move it to the league column.

#### ii. Create Country column for famous Leagues
I found while exploring that some famous league with highest turnover and number of bets were present without the country name. So, I added them manuallly.

#### iii. Event Start Date
The Event start date for the same event ID is wrong many times, and created a floor for seconds and merged all the event start dates with respect to Event ID when they are few seconds apart. Other than that, if the event start dates for same event ID has a large difference, then I group by event ID and perform aggregation on all the columns. 

#### iv. Sessions with No Number of Bets
For convenience, I removed all the data points if there are no number of bets. 

### Use cases
I have considered few ML based use cases, and some more statistical use cases with the given data. 
 
 * Number of Bets Next hour
 * Peak Hour Classification for the day
 * Team and League popularity
 * Identify Lease Enagaging hours in a day
 * Turn Over In Eur Statistics for Prematch vs Live Betting



#### Number of Bets for the next hour
    I have created many features to make the prediction of number of bets next hour. One of the important features are rolling sum of number of bets for the specific event in the last 3 hours, rolling average of number of bets in the whole league in the last 7 days. And then created also a target feature Next_hour_bet. 

Below is the feature correlation matrix for the above use case where correlation between feature pairs are calculated and one of the highly dominant feature pairs are removed. 

![matrix](Images\matrix_3.png)

Below is the feature importance for the above Use case based on random forest regressor fitting. 

![FI](Images\FI_nexthour.png)

I have tried XG Boost, Ensemble Model containing (RF and XGB), and also NN model through MLP. 

 #### <ins>To do in the future:</ins>
 Because of time constraints, I was unable to achieve many things. The results are not the best when I tried these models, I would have tried to perform hyperparameter runing in many of these models using Optuna or Grid Search CV, and brought the losses down. ¨

 One more task to perform in the future is perform more transformations in the columns, add new features, and eliminate some redundant features. 


#### Peak Hour Classification for the day

    The idea behind this task is to predict which hour of the day is the most peak hour of the day given a data point, so that company can plan for a bigger traffic at the peak time and plan for better management of resources, allocate more customer care representatives, and also try to engage customers though different forms of promotions at this time, since the chances of making a bet is higher at these times. 

Here you can see in general when in time per day, the most number of bets are placed.

![FI](Images\peak_bar.png)

The multiclass classification model is created to classify the peak hour based on the given data point, and league, and country, betting day, if the event is in week day or week end. 

I have tried XGBoost Classifier to classify and predict the peak hours, and performed Shapely Additive Explanations to show if a particular feature has a positive or negative impact in the classification and also how much is that impact. 0 means no impact. And each point here is each data point.

![FI](Images\shap.png)

 #### <ins>Evaluation:</ins>

We are successfully able to identify the peak hours in a day based on various features. The evaluation metrics are given below:

![FI](Images\results_4.png)

 <strong>The confusion matrix is also provided for different classifications.</strong>

![FI](Images\cm.png)







