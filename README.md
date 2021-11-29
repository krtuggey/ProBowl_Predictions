# NFL Pro Bowl Analysis

The Final Project for the [UT Data Analysis and Visualization Boot Camp](https://techbootcamps.utexas.edu/data/).

Group repository: https://github.com/krtuggey/ProBowl_Predictions

Contributors:
- https://github.com/patels250
- https://github.com/Bionicbabes
- https://github.com/krtuggey

## Communication Protocols
Our team communicated through Slack, Zoom, Text, and Github.

## Project Topic: NFL Pro Bowl Data Analysis
### Reason

During the initial phase of the project and project brainstorming, the team focused on topics that met certain criteria:
- Interesting context and marketable application
- The initial datasets were easily accessible and up to date
- The final project could be completed in a feasible amount of time
- Team members were comfortable with their roles within the project

The NFL Pro Bowl was chosen as the project focus because:
- The process is interesting and demonstrates the principles we have learned throughout the course
- The data available was vast and accessible
- A machine learning model can be applied effectively

## Source Data Overview

For this analysis, six sets of data from 2019 and 2020 were pulled, cleaned and combined to begin building a linear regression model. 
- 2019 source data: 
  - [2019 NFL Rushing](https://www.pro-football-reference.com/years/2019/rushing.htm)
  - [2019 NFL Passing](https://www.pro-football-reference.com/years/2019/passing.htm)
  - [2019 NFL Receiving](https://www.pro-football-reference.com/years/2019/receiving.htm)
  - [2019 NFL Pro Bowl](https://www.pro-football-reference.com/years/2019/probowl.htm)
- 2020 source data:
  - [2020 NFL Rushing](https://www.pro-football-reference.com/years/2020/rushing.htm)
  - [2020 NFL Passing](https://www.pro-football-reference.com/years/2020/passing.htm)
  - [2020 NFL Receiving](https://www.pro-football-reference.com/years/2020/receiving.htm)
  - [2020 NFL Pro Bowl](https://www.pro-football-reference.com/years/2020/probowl.htm)

The data can answer the question: "Can we use historical NFL statistics to effectively predict future Pro Bowl players?"

## Dataset

- Data downloaded from Pro Football Reference as .xlsx files
- Data processed and cleaned in Pandas
- Data exported as .csv files
- Data from .csv files loaded into PostgreSQL using pgAdmin4 and uploaded to AWS RDS

![ERD.PNG](Resources/Images/ERD.PNG)

- 545 players in 2019, 561 players in 2020
- 22 variables
  - Player
  - Team
  - Age
  - Position 
  - Games Played
  - Games Started
  - Pass Completions
  - Pass Attempts
  - Pass Yards
  - Pass Touchdowns
  - Interceptions
  - 4th Quarter Comebacks
  - Game Winning Drives
  - Rush Attempts
  - Rush Yards
  - Rush Touchdowns
  - Targets
  - Receptions
  - Receiving Yards
  - Receiving Touchdowns
  - Fumbles
  - Pro Bowl (True/False)

## Machine Learning Model

------------------------------------

**Summary**

- After investigating our data and understanding that our goal was to create a model that would be able to predict future outcome of a given data set we decided to choose the supervised machine learning logistic regression model.  In past experience we used sklearn on a single data set implementing the train_test_split function.  This function will take the data and randomly split the data into the test and train data sets but that is not what we wanted to do.  For our model we wanted to use the 2019 data set as our training model and 2020 data set as our testing model to see how well we are able to predict future pro bowl selections based on player statistics.  The below is a step by step analysis for the QB position and the analysis was repeated for each position RB,WR and TE. 

**Preparign the Data**

- When we pulled in the data from the data base there was some manipulation that needed to be done because Scikit-learn's algorithms only understand numeric data.  The data had multiple columns that contained characters so we had a decision to make to either keep the data or just remove the data, we ended up doing a little of both.  One technique to do this is to encode the data or we could have used a the function labelencoder.  The decision was made that the team that the player played for was insignificant and that data could just be removed, also we decided to splits all the players into their own data set based on position.  Therefore the position had no significance if they were all the same for all the players.  We then just indexed all the player names in the data set and we were left with a clean numerical data set that we could perform our logistical regression on.  

**Original Data Set** 
![preparing_data_1.PNG](https://github.com/krtuggey/ProBowl_Predictions/blob/main/Resources/Images/preparing_data_1.PNG)

**Cleaned Data Set**

![preparing_data_2.PNG](https://github.com/krtuggey/ProBowl_Predictions/blob/main/Resources/Images/preparing_data_2.PNG)

### Splitting the data

- Next step with the logisitical regression is to split the data into you X_train, Y_train, X_test, Y_test.  For our predictive model we wanted to take all the player statistics and make them into our X_train and our outcome will be whether or not the player made the pro bowl or not. 

**2019 data set X_train, Y_train**

![splitdata_2019.PNG](https://github.com/krtuggey/ProBowl_Predictions/blob/main/Resources/Images/splitdata_2019.PNG)

**2020 data set X_test, Y_test**

![splitdata_2020.PNG](https://github.com/krtuggey/ProBowl_Predictions/blob/main/Resources/Images/splitdata_2020.PNG)


## **Logistic Regression**
- Once all the variable were assigned for the model we were able to run the model and get our results using the classifer.predict on your X_test data set. We were able to get an accuracy score by comparing the predicted values vs. y_test values. 
- Our model was able to predict with 92.5 % accuracy 

![logisitic_regression.PNG](https://github.com/krtuggey/ProBowl_Predictions/blob/main/Resources/Images/logisitic_regression.PNG)

## **Random Forest Clasifier**
- We also wanted to do more analysis to try and figure our which of the feature are the most significant and to see if the we could get better accuracy with another model.  Determining the most significant feature will help us later in creating our dashboard.  After running the analysis we found our some interesting information from the confusion matrix and that statistics. 
- Accuracy in the random forest classifier was reduced to 90%
- For the QB predictions the recall was 0, meaning it was not able to predict and of the probowl player in the 2020 data set.
- The recall for each position ranged from 0% to 75% 

**Confusion Matrix**

![confusion%20matrix.PNG](https://github.com/krtuggey/ProBowl_Predictions/blob/main/Resources/Images/confusion%20matrix.PNG)

## **Importances**
- To find our which features in the data set were of the most importance we used the Mean Decrease in Impurity function.  Gini Importance or Mean Decrease in Impurity (MDI) calculates each feature importance as the sum over the number of splits (across all tress) that include the feature, proportionally to the number of samples it splits.

![importances_MDI.PNG](https://github.com/krtuggey/ProBowl_Predictions/blob/main/Resources/Images/importances_MDI.PNG) 

## **Improtance Permutations**
- With the data above we could see how each of the features were weighted in the random forest classifier model but it was still unclear which feature is the most significant.  To help us better identify the feature with the most impact we used Permutation feature importance.  The permutation feature importance is defined to be the decrease in a model score when a single feature value is randomly shuffled.  This procedure breaks the relationship between the feature and the target, thus the drop in the model score is indicative of how much the model depends on the feature. This technique benefits from being model agnostic and can be calculated many times with different permutations of the feature.

![permutation_importance.PNG](https://github.com/krtuggey/ProBowl_Predictions/blob/main/Resources/Images/permutation_importance.PNG)

## **Results**
- The results we very mixed, although our accuracy was really good all of them being above 90% our recall was between 0% and 75% and we would like to refine the model to get the recall to be more consistent.  
- To make this model more robust we would go back 5 year instead of just 1 year 
- Create a threshold on player statistics removing the outliers creating a more standard scaler
- Limit to amount of feature to remove items like age, games, games started.


## Presentation

[Google Slides Presentation](https://docs.google.com/presentation/d/1QMTFeos1eDaJR3Kg4zpU0v_xQqYuAL53f5qtuI3LXi4/edit?usp=sharing)

## Dashboards

[2019 Dashboard](https://public.tableau.com/app/profile/sagar.patel4941/viz/ProBowl2019/2019Dashboard)

[2020 Dashboard](https://public.tableau.com/app/profile/sagar.patel4941/viz/ProBowl2020/2020Dashboard)
