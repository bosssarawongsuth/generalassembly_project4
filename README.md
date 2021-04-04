# GA Project 4 - Kaggle West Nile Virus Prediction
## Fong, Gip, Boss

## Background

West Nile Virus (WNV) is one of the most commonly spread to humans through infected mosquitos. A mosquito catches this disease by biting birds such as infected American robins, gray catbirds, or house sparrows. Approximately 20% of infected people develop symptoms ranging from a persistent fever to serious illnesses that can result in death. People over the age of 70 and with chronic conditions such as weakened immune systems or high blood pressure are at most risk if they are infected with West Nile virus. 

Chicago has experienced one of the highest levels of West Nile virus risk in this decade. In 2002, the first human cases of West Nile virus were reported in Chicago. By 2004, the City of Chicago and the Chicago Department of Public Health (CDPH) had established a comprehensive surveillance and control program that is still in effect today. Every year from late-May to early-October, public health workers in Chicago setup mosquito traps scattered across the city. Every week from Monday through Wednesday, these traps collect mosquitos, and the mosquitos are tested for the presence of West Nile virus before the end of the week. The test results include the number of mosquitos, the mosquitos species, and whether or not West Nile virus is present in the cohort. 

## Problem Statement
As a team of data scientists from the Chicago Department of Public Health (CDPH), we are tasked with building a model that can help accurately predict when and where different species of mosquitos will test positive for WNV, using weather, location, testing, and spraying data.

The model should help the City of Chicago and CDPH more efficiently and effectively allocate resources towards preventing transmission of this potentially deadly virus.

### Datasets

### Data Dictionary

The data provided are the locations of West Nile virus (train & test datasets) , the locations where mosquitoes repellent spray was used (spray dataset) , and the weather of the days (weather dataset). The training set consists of data from 2007, 2009, 2011, and 2013, while in the test set you are requested to predict the test results for 2008, 2010, 2012, and 2014. The spray dataset consists of GIS data of spraying efforts in 2011 and 2013. The weather dataset consists of data from 2007 to 2014.


| Feature                      | Variable type | Datatype | Dataset            | Description                                                                     |
|------------------------------|---------------|----------|--------------------|---------------------------------------------------------------------------------|
| id                           | Norminal      | int64    | test               | The id of the record                                                           |
| date                         | Datetime      | datetime | train and test     | Date that the WNV test is performed                                             |
| species                      | Norminal      | object   | train and test     | Species of mosquito                                                             |                                         |
| trap                         | Norminal      | object   | train and test     | Id of the trap                                                                  |                           |
| latitude                     | Continuous    | float64  | train and test     | Latitude  returned from GeoCoder                                                |
| longitude                    | Continuous    | float64  | train and test     | Longitude returned from GeoCoder                                                |                   |
| nummosquitos                 | Discrete      | int64    | train and test     | number of mosquitoes caught in this trap                                        |
| wnvpresent                   | Discrete      | int64    | train and test     | whether WNV was present in these mosquitos. 1 means WNV is present, and 0 means not present.                                |
| year                         | Discrete      | int64  | train and test     | Year that the WNV test is performed                                            |
| month                        | Discrete      | int64   | train and test    | Month that the WNV test is performed                                            |
| weekofyear                   | Discrete      | int64   | train and test    | Week of year that the WNV test is performed                                    |
| yearmonth                    | Discrete      | int64   | train and test    | Year and month that the WNV test is performed                                  |
| station                      | Discrete      | int64    | weather            | Station 1 or 2 where weather data is collected                                  |
| date                         | Datetime      | datetime | weather            | Date of weather record                                                          |
| tmax                         | Discrete      | int64    | weather            | Maximum temperature in Fahrenheit                                                   |
| tmin                         | Discrete      | int64    | weather            | Minimum temperature in Fahrenheit                                                   |
| tavg                         | Continuous    | float64  | weather            | Average temperature in Fahrenheit                                                   |
| depart                       | Discrete      | float64  | weather            | The difference from normal temperatures for the last 30yrs                      |
| dewPoint                     | Discrete      | int64    | weather            | Average Dew Point temperature in Fahrenheit                                                          |
| wetBulb                      | Discrete      | int64    | weather            | Average Wet Bulb temperature in Fahrenheit                                                          |                          |
| sunrise                      | Datetime      | datetime | weather            | Sunrise time                                                                 |
| sunset                       | Datetime      | datetime | weather            | Sunset time                                                                  |                                                            |
| preciptotal                  | Continuous    | float64  | weather            | The depth of rainfall/melted snow in inches                                               |                                                         |
| resultspeed                  | Continuous    | float64  | weather            | Resultant wind speed                                                            |
| resultdir                    | Continuous    | int64    | weather            | Resultant wind direction                                                        |
| avgspeed                     | Continuous    | float64  | weather            | Average wind speed                                                                  |
| daytime                      | Continuous    | float64  | weather            | Number of hours of sunlight for each day                                                              |
| date                         | Datetime      | datetime | spray              | Date of the spray                                                               |
| time                         | Datetime      | datetime | spray              | Time of the spray                                                               |
| latitude                     | Continuous    | float64  | spray              | Latitude of the spray                                                           |
| longitude                    | Continuous    | float64  | spray              | Latitude of the spray                                                           |

### Evaluation

|  ROCAUC Score  |LogisticRegression|RandomForest|ExtraTree      |XGBoost        |
|----------------|---------------| -----------    | ----------   |--------------|
| Training       | 0.888        | 0.884         | 0.861         | 0.930         |
| CV             |0.837         | 0.856         | 0.839         | 0.867         |
| Validation     | 0.830         | 0.846         | 0.825         | 0.846         |
| Testing/Kaggle | 0.756          | 0.709         | 0.720         | 0.695         |

The model that scored the highest ROCAUC is XGBoost, followed by Random Forest, Logistic Regression and Extra Tree. However, the differences are very small differing by only around 0.01. However, when it comes to scoring on Kaggle on the testing set, XGBoost performed the worst compared to the other models. This could be attributed to the fact that XGBoost suffers from high variance resulting in bad generalisation. On the testing set, Logistic Regression seems to be more generalised (lower variance). The model scored the best on the testing/Kaggle data with the ROCAUC score of 0.756 and thus we will consider this model to be the most useful for the purpose of this study.

### Conclusion
With our goal to predict when and where different species of mosquitoes will test positive for WNV, we created several classification models to predict the presence of the virus. Among all the regression algorithms that we used, we found that Logistic Regression performed well compared than other model and the baseline. Given that it seems to be more generalised (lower variance) than other models, it scored the best on the testing data with the ROCAUC score of 0.756 and thus we will consider this model to be the most useful for this study.

Out of all the predictors for the model, we found that average temperature was the top predictor with the exponential coefficient at about 160. On the other hand, location was not a strong predictor in our best model, but weather and week of year were more important features.

Regarding cost benefit analysis, we found that the spray should be used to reduce number of mosquitos. Additionally, the spray cost for Chicago would be \\$900,000 and the total cost for the infected person would be \\$28,570. Hence, the spray cost will cover only 30 severe WNV cases. The target areas from the model have the total area at 50.5 square kilometer which requires \\$74,300 of spray cost. If the spray were to be used, Chicago Council should spray more in summer (August) because this month had more risk of WNV in human from the virus-carrying mosquitoes

### Recommendations
- The sub-urban in Chicago has more risk from WNV due to the poor sanitation system in the older houses compared to new houses [[Source]](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC7241786/). Therefore, the Chicago council should give the sanitation maintenance to the old houses.
- We recommend to always spray to prevent the high medical cost and economic loss, and the spray help Chicago to prevent the unpredictability of WNV outbreaks in people










