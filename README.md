# Capstone Project: Using  a Batter's Offensive stats to Predict Their Last Season Played HR's, RBI's and AVE

## Author: Mario Sanchez, Jr.
## Date: 8/25/2019


# Question:

Can regression models be created to accurately predict a players HR's, RBI's and AVE of their last season played?

# Objectives:

- Obtain baseball data from trusted sources
- Learn how to aggregate the multiple csv files into the form I need
- Pick multiple regression models and compare their performance on unseen data
- Which model performed best for each metric (HR's, RBI's, AVE)?
- How can we use this information to improve our ability to predict a players performance using historic data?


# Data Description:

- Batting.csv
- People.csv
- retrosplits
- Most of the data in the Databank is provided by Chadwick Baseball Bureau
(http://www.chadwick-bureau.com).  The data differ from the data the Bureau provides
to its clients in that it contains less detail, is updated less frequently, 
and is provided on an as-is basis.

The Databank is historically based in part on the Lahman Baseball Database, 
version 2015-01-24, which is Copyright (C) 1996-2015 by Sean Lahman.

The tables Parks.csv and HomeGames.csv are based on the game logs
and park code table published by Retrosheet.
This information is available free of charge from and is copyrighted
by Retrosheet.  Interested parties may contact Retrosheet at 
http://www.retrosheet.org.

- batter_and_change_FINAL DataFrame has 41,745 rows and 84 columns
- previous_years_FINAL DataFrame has 38,908 rows and 84 columns
- last_year_df_FINAL DataFrame has 2837 rows and 84 columns


# Data Dictionary:

| Columns Name | Description                |
|--------------|----------------------------|
| playerID     | unique identifier          |
| yearID       | year for that row          |
| teamID       | team played on             |
| stint        | stint                      |
| G            | games played               |
| AB           | at-bats                    |
| R            | runs                       |
| H            | hits                       |
| 2B           | doubles                    |
| 3B           | triples                    |
| HR           | homeruns                   |
| RBI          | runs batted in             |
| SB           | stolen bases               |
| CS           | caught stealing            |
| BB           | base on balls              |
| SO           | strike out                 |
| IBB          | intentional walk           |
| HBP          | hit by pitch               |
| SH           | sacrifice hit              |
| SF           | sacrifice fly              |
| GIDP         | grounded into double plays |
| nameFirst    | first name                 |
| nameLast     | last name                  |
| bats         | left or right              |
| throws       | left or right              |
| debut        | first year played          |
| finalGame    | last year played           |
| _percent     | percent spent in that era  |
| era_         | binary era                 |
| decade_      | binary decade              |
| throws_R     | 1 if throws R              |
| bats_R       | 1 if bats R                |
| AVE          | average                    |
| OBP          | on base percentage         |
| Slug_Percent | slugging percentage        |
| OPS          | on base + slugging         |
| debutYear    | first year played          |
| currentYear  | year of that row           |
| YRSPRO       | experience                 |
| _chg         | change from previous year  |
| KMeans_label | cluster label              |


## Sources: 
1. https://medium.com/@williamkoehrsen/data-analysis-with-python-19434f5d6324
2. http://www.seanlahman.com/baseball-archive/statistics/
3. https://www.datacamp.com/community/tutorials/scikit-learn-tutorial-baseball-1
4. https://www.datacamp.com/community/tutorials/scikit-learn-tutorial-baseball-2
5. https://github.com/WillKoehrsen/Udacity-Data-Analyst-Nanodegree
6. http://www.baseballdatascience.com/


## Target: Last Year HR's, RBI's and HR's

# EDA and Model Selection:

1. Obtained historical baseball data from many online resources.

2. After exploring many of the files available I decided to use the one which contained each players stats divided by years.

3. Combined the batting.csv with people.csv to obtain vital information on each player.

4. Grouped my data by player, year and team.

5. Filtered my dataframe to only include batters who had at least 20 games played and 20 ab-bats.

6. Next I wrote a function to include only players who had at least 5 years played in the MLB.

7. I then filtered my dataframe one last time to include only players who appeared after 1900.

8. Feature Engineering:

- Wrote a function to assign an era label to each player dependent on when they played the game and then what percentage of their career they played in that era.

- Assigned a year label to each player and created dummy columns from these labels.

- Assigned a decade label to indicate which decades the player had played in.

- The above columns were created to account for the different era's that have occurred over the last 119 years.

- Created a binary column to indicate if a player batted and threw right handed.

- Created AVE, OBP, Slug_Percent, and OPS columns.

- Computed a players experience by subtracting the current year from the debut year.

9. Split my final dataframe into previous years and final year so that I can test my models on unseen data and compare their results.

4. Model Preparation:

- Used previous years to train and test on
- Made sure that columns such as G, H, AB were left out
- Scaled my train, test and unseen data for some of the regression models
- Created polynomial features to my X variable to provide more data to my models
- Grid search over several parameters for each model

6. Models:

- For each target, HR's, RBI's, and AVE, I fit each of the following models:
- Linear Regression
- Ridge
- Lasso
- ElasticNet
- RandomForest

# Model Performance:

After many different iterations, the following models were tested with above features to determine which performed best using the R2 score and RMSE.

1. Predicting AVE:

Linear Regression Train R2 Score: 0.927265749628238
Linear Regression Test R2 Score: 0.9245850874144554
Ridge Train R2 Score: 0.9641036826810402
Ridge Test R2 Score: 0.9501996596045186
Lasso Train R2 Score: 0.9167955525718006
Lasso Test R2 Score: 0.9140641297211587
ElasticNet Train R2 Score: 0.9471689658637862
ElasticNet Test R2 Score: 0.9453456477932288
Random Forest Train R2 Score: 0.9935941144091776
Random Forest Test R2 Score: 0.9543081856108968
Linear Regression RMSE on New Data: 0.022072780140648625
Ridge RMSE on New Data: 0.0323865503500996
Lasso RMSE on New Data: 0.03298153698364595
ElasticNet RMSE on New Data: 0.030976570580385922
Random Forest RMSE on New Data: 0.016747452199047858
Linear Regression R2 Score on New Data: 0.8157356416523764
Ridge R2 Score on New Data: 0.6033050721934583
Lasso R2 Score on New Data: 0.5885954929121789
ElasticNet R2 Score on New Data: 0.6370941785539136
Random Forest R2 Score on New Data: 0.893922137971072

2. Predicting RBI's:

Linear Regression Train R2 Score: 0.9282337759628065
Linear Regression Test R2 Score: 0.9311742490423233
Ridge Train R2 Score: 0.9493429034345244
Ridge Test R2 Score: 0.9430190274928
Lasso Train R2 Score: 0.94951401869399
Lasso Test R2 Score: 0.9465989701115267
ElasticNet Train R2 Score: 0.9218334693805789
ElasticNet Test R2 Score: 0.9250505846389491
Random Forest Train R2 Score: 0.9887318112663641
Random Forest Test R2 Score: 0.9362520045126567
Linear Regression RMSE on New Data: 5.526281075333878
Ridge RMSE on New Data: 26.189041645368615
Lasso RMSE on New Data: 25.380538043708153
ElasticNet RMSE on New Data: 24.269181261146084
Random Forest RMSE on New Data: 5.213557078014037
Linear Regression R2 Score on New Data: 0.8801086958714287
Ridge R2 Score on New Data: -1.6925325162640654
Lasso R2 Score on New Data: -1.5288518836501495
ElasticNet R2 Score on New Data: -1.3122351284302
Random Forest R2 Score on New Data: 0.8932937127367198

3. Predicting HR's:

Linear Regression Train R2 Score: 0.9123830309085669
Linear Regression Test R2 Score: 0.911395154652938
Ridge Train R2 Score: 0.9839560929298725
Ridge Test R2 Score: 0.9810375920991171
Lasso Train R2 Score: 0.9895424128271637
Lasso Test R2 Score: 0.9873949398289043
ElasticNet Train R2 Score: 0.8732944355681218
ElasticNet Test R2 Score: 0.873122027197329
Random Forest Train R2 Score: 0.9914084916509395
Random Forest Test R2 Score: 0.9565788564133643
Linear Regression RMSE on New Data: 2.1945386661296733
Ridge RMSE on New Data: 6.871186887441323
Lasso RMSE on New Data: 6.6806050835395405
ElasticNet RMSE on New Data: 5.7251772746060565
Random Forest RMSE on New Data: 0.9997683023791144
Linear Regression R2 Score on New Data: 0.6736586218690606
Ridge R2 Score on New Data: -2.199257455812315
Lasso R2 Score on New Data: -2.024247067469625
ElasticNet R2 Score on New Data: -1.221076649274769
Random Forest R2 Score on New Data: 0.932269482244308


# Primary findings/conclusions/recommendations:

- The RandomForest Regression model performed the best on predicting all metrics. 
- Many of the models performed well on test data but poorly on unseen data.
- This indicated to me that using an ensemble model was a better approach at more accurately predicting my targets.
- I believe that I can achieve even better results if I log transform my target variable since there is a skewed distribution.
- This information can then be leveraged to direct scouting reports and help teams better evaluate their players performance. These models allow for a players past history as well as others from around the league to determine what type of batter they are.
- This can then allow for a better forecast of a teams performance broken down by player.


# Limitations and Assumptions:

- More feature engineering can improve the models.
- It is possible that there may have been some data leakage, further investigation is needed.
- Computing power becomes an issue when fitting certain models. This greatly influences how much tuning can go into each model.
-The results are encouraging and I believe they can by extended to predict many other offensive metrics.


# Future Analysis:

- Explore other models such as ExtraTreesRegressor, AdaBoostRegressor and BaggingRegressor
- Test models on other offensive metrics such as OBP, or Slugging Percent and see I they can generalize well to these metrics.
-Test the models on select subsets of players such as by position or by era. This may reveal very interesting findings. 
- There is truly a mountain of available data for baseball as well as other sports and am excited to apply what I have learned in this project to future projects.
