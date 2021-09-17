# Machine Learning Project : Pump it Up: Data Mining the Water Table 
- Github link : https://github.com/Hacko97/MLProject_Pump_it_Up_Data_Mining_the_Water_Table
- Competiton link: https://www.drivendata.org/competitions/7/pump-it-up-data-mining-the-water-table/
- Accuracy of best model : 0.8251
- Final Rank : 261(As of 17th September 2021)

## Introduction
This project is a multi-class classification problem. The goal is to predict which pumps are working, which need repair, and which are not working at all. To solve this problem, the data will be loaded and explored to address its quality and apply the data cleansing method to get ordered data. The data will be used to train a classifier based on the method of random forests. Finally, the model will be tested on a cross-validation dataset before predicting which classes of the given test dataset should be submitted to the competition website.
## Exploratory Data Analysis
- The dataset is not balanced. ‘Functional’ > ‘Non-functional’ > ‘Functional but it needs repair’. “Accuracy” is metric used in the competition. We need to solve data imbalance. because model prediction gets biased. The initial strategy had been to analyze each characteristic individually and also in a group of related features according to its characteristics.
- categorical features:
  - region_code: there are some outliers with log transformation the problem can be solved
  - district_code: there are some outliers but the log transform can solved
  - funder: 3635 missing values, a lot of categories
  - installer: 3655 missing values, a lot of categories
  - wpt_name: a lot of categories there are some None values
  - payment: limited categories no sign for missing values
  - payment_type: limited categories no sign for missing values (there are some 0s)
  - Water_quality: limited categories no sign for missing values (there are some 0s)
  - Quality_group: limited categories no sign for missing values (there are some 0s)
  - Source: limited categories no sign for missing values (there are some 0s)
  - Source_type: limited categories no sign for missing values (there are some 0s) (high correlated with source)
  - source_class: a lot of 0s-->unknown
  - Waterpoint_type: limited categories no sign for missing values (there are some 0s)
  - Waterpoint_type_group: limited categories no sign for missing values (there are some 0s)
  - Basin: limited categories no sign for missing values
  - Sub village:a lot of categories there are no signs of missing values
  - region: limited categories no sign for missing values
  - Lga: a lot of categories there are no signs of missing values
  - Ward: a lot of categories there are no signs of missing values
  - public_meeting:3334 missing values: limited categories there are some signs for missing values (there are some 0s and -1)
  - recorded_by: one value no variation
  - scheme_management: 3877 missing values limited categories
  - scheme_name: 28166 missing values lot of categories
  - permit:3056 missing value two categories
  - Extraction_type: limited categories no sign for missing values
  - extraction_type_group:limited categories no sign for missing values
  - extraction_type_class:limited categories no sign for missing values
  - Management: limited categories no sign for missing values
  - Management_group: limited categories no sign for missing values
  - Quantity: limited categories no sign for missing values
  - Quantity_group: limited categories no sign for missing values
- Numerical features :
  - amount_tsh: the amount of water: it contains 0s as invalid values. nonlinear transformation does not help to remove the 0 values
  - gps_height: the values look ok no invalid values (it is not possible to tell if the 0s are invalid values)
  - longitude: there are some 0 values as invalid values and they should be replaced
  - latitude: No sign of invalid values
  - population: there are some zeros as invalid values
- Special features:
  - id: unique number refers to a certain pump.
  - construction_year: there are some zeros that are invalid data that should be replaced
  - num_private: there are some large values. they look like outliers. it contains a large number of 0s as invalid values
  - date_recorded: will change to datestamp 

## Feature Engineering and preprocessing
- The date will be changed so it can be used as numerical values
- *Amount_tsh* feature which is the total static load (quantity of water available at the water point), is skewed, which is why the log was used to smooth it.
- Features *region_code, district_code, gps_height, num_private, population, construction_year* which are smooth by log. 
- Some functionalities had been created as part of the feature engineering part. The first case was related to the *construction_year* date, which had been subtracted from the *date_recorded*, in order to identify the operational years of these wells, and also in the case of the amount of well water related to the population, it had been divided amount_tsh by population, in these cases certain treatments had been carried out at the beginning. By the way, it was found that the older the water pump, the more repair it will require.
- *Recorded_by,source_type, waterpoint_type_group, scheme_name, extraction_type_class , quantity_group* features are drop because that are high correlated with other columns or they have large amount of missing values.


## Model
- Experimenting with different classification algorithms
  - Random forest
  - Decision Trees
  - K-Nearest Neighbors
  - XG boost
  - SVM
  - Logistic regression
- After experimenting with different algorithms random Forrest performs best.
- best hyperparameters values: RandomForestClassifier(bootstrap=True, class_weight=None, criterion='gini', max_depth=22, max_features='auto', max_leaf_nodes=None, min_impurity_decrease=0.0, min_impurity_split=None, min_samples_leaf=1, min_samples_split=2, min_weight_fraction_leaf=0.0, n_estimators=600, n_jobs=1,oob_score=False, random_state=0, verbose=0, warm_start=False) 


## Proof of submission
DrivenData username: moracse_170141X

![This is an image](https://github.com/Hacko97/MLProject_Pump_it_Up_Data_Mining_the_Water_Table/blob/main/proof_of_submission.png)






