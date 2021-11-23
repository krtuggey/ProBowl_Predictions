# NFL ProBowl Analysis

The Final Project for the [UT Data Analysis and Visualization Boot Camp](https://techbootcamps.utexas.edu/data/).

Group repository: https://github.com/krtuggey/ProBowl_Predictions

Contributors:
- https://github.com/patels250
- https://github.com/Bionicbabes
- https://github.com/krtuggey

## Communication Protocols
Our team communicated through Slack, Zoom, Text, and Github.

## Project Topic: NFL ProBowl Data Analysis
### Reason

During the initial phase of the project and project brainstorming, the team focused on topics that met certain criteria:
- Interesting context and marketable application
- The initial datasets were easily accessible and up to date
- The final project could be completed in a feasible amount of time
- Team members were comfortable with their roles within the project

The NFL ProBowl was chosen as the project focus because:
- The process is interesting and demonstrates the principles we have learned throughout the course
- The data available was vast and accessible
- A machine learning model can be applied effectively

## Source Data Overview

For this analysis, six sets of data from 2019 and 2020 were pulled, cleaned and combined to begin building a linear regression model. 
- 2019 source data: 
  - [2019 NFL Rushing](https://www.pro-football-reference.com/years/2019/rushing.htm)
  - [2019 NFL Passing](https://www.pro-football-reference.com/years/2019/passing.htm)
  - [2019 NFL Receiving](https://www.pro-football-reference.com/years/2019/receiving.htm)
- 2020 source data:
  - [2020 NFL Rushing](https://www.pro-football-reference.com/years/2020/rushing.htm)
  - [2020 NFL Passing](https://www.pro-football-reference.com/years/2020/passing.htm)
  - [2020 NFL Receiving](https://www.pro-football-reference.com/years/2020/receiving.htm)

#### Questions we hope to answer
- Using historical NFL statistics and a machine learning model, are we able to predict which player will make the ProBowl?
- Can player statistics provide the necessary data to make a machine learning model? If not, is there a better source of data?

#### Sources and tools
- Project data is from https://www.pro-football-reference.com/ 
- We are using three datasets from 2019 and 2020: passing, rushing, and receiving. These datasets will be cleaned and used as training data.
- Additionally, the 2019 and 2020 ProBowl list of players is used as a reference to test predictions.

#### Communication protocols
- Square role  - Kat
- Triangle role  - Soren
- Circle role  - Sagar
- 

#### Machine Learning Model
- Can be seen in "Pro_Bowl_Predictors.ipynb"

#### Database
- Databases are found in the "Resources" folder
- "Data_Cleaning.ipynb" is used for cleaning and transforming.
