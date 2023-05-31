# Report: Predict Bike Sharing Demand with AutoGluon Solution
#### Tatenda Chirima

## Initial Training
### What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?
Observation: While submitting predictions obtained from all these five experiments, some of the experiments delivered negative predictions values.
Changes incorporated: Kaggle refuses the submissions containing negative predictions values obtained from the predictor. Hence, all such negative outputs from respective predictors were replaced with 0.

### What was the top ranked model that performed?
The model with the highest validation RMSE score of 33.9236 and the best Kaggle score of 0.44368 (on test dataset) was WeightedEnsemble_L3. This model was created without the assistance of a hyperparameter optimisation method by training on data gathered through exploratory data analysis (EDA) and feature engineering. Some models improved their RMSE scores on validation data after hyperparameter optimisation; nevertheless, this model performed best on an unknown test dataset. Because many models provided competitive performance, the selection was made using both RMSE (cross-validation) and Kaggle (test data) ratings.

## Exploratory data analysis and feature creation
### What did the exploratory analysis find and how did you add additional features?
To retrieve hour information from timestamps, feature datetime was processed as a datetime feature.
Season and weather were first viewed as integer characteristics. Because they are categorical variables, they were converted to the category data type.
Using feature extraction, the data for the year, month, day (dayofweek), and hour were retrieved as different independent features from the datetime feature. The datetime feature was removed during feature extraction.
After investigating and examining the casual and registered characteristics, it was discovered that the RMSE scores increased dramatically during cross-validation and that these independent features were closely connected to the target variable count. However, the casual and registered characteristics are only available in the train dataset and not in the test data, therefore they were ignored/dropped during model training.

Day_type, a category feature based on holiday and workingday, was introduced. It was designed to effectively separate the categories of "weekday," "weekend," and "holiday."
Furthermore, the correlation between characteristics temp (temperature in degrees Celsius) and atemp ('feels like' temperature in degrees Celsius) was 0.98. As a result, atemp was removed from the train and test datasets to decrease multicollinearity between independent variables.
Data visualisation was also used to get insights from the characteristics.


### How much better did your model preform after adding additional features and why do you think that is?
In comparison to the initial/raw model performance (without EDA and/or feature engineering), the inclusion of extra features enhanced model performance by around 175%.
After transforming specific categorical variables having integer data types into their genuine categorical datatypes, the model performance increased.
Aside from omitting casual and registered characteristics during model training, atemp was removed from the datasets since it was substantially linked with another independent variable, temp. This aided in the reduction of multicollinearity.
Furthermore, splitting the datetime feature into multiple independent features such as year, month, day, and hour, as well as the addition of day_type, improved model performance because these predictor variables help the model more effectively assess seasonality or historical patterns in the data.


## Hyper parameter tuning
### How much better did your model preform after trying different hyper parameters?
Tuning the hyperparameters was advantageous since it improved the model's performance over the first submission. When undertaking hyperparameter optimisation tests, three distinct setups were employed. Although hyperparameter optimised models performed similarly to the model with EDA and additional features, the latter performed significantly better on the Kaggle (test) dataset.


Discussion:

When training with the autogluon package, the recommended parameters were taken into consideration. The performance of hyperparameter optimised models, on the other hand, was suboptimal since the hyperparameters are tuned using a predetermined set of values provided by the user, limiting the alternatives autogluon may investigate.
Furthermore, while doing hyperparameter optimisation with autogluon, the 'time_limit' and 'presets' parameters are quite important.

As a result, lighter and quicker default alternatives such as'medium_quality' and 'optimized_for_deployment' were tested. As the rest of the presets failed to construct models using AutoGluon for the testing setups, I picked the quicker and lighter "optimize_for_deployment" for hyperparameter optimisation method.
The most difficult challenge when utilising AutoGluon with a predefined range of hyperparameters is deciding between exploration and exploitation.


### If you were given more time with this dataset, where do you think you would spend more time?
I'd want to study more potential outputs when AutoGluon is run for an extended length of time with a high quality preset and better hyperparameter tweaking if I had more time to work with this dataset.


### Create a table with the models you ran, the hyperparameters modified, and the kaggle score.


### Create a line plot showing the top model score for the three (or more) training runs during the project.

File in img folder

![model_train_score.png](img/imodel_train_score.png)

### Create a line plot showing the top kaggle score for the three (or more) prediction submissions during the project.

File in img folder

![model_test_score.png](img/model_test_score.png)

## Summary
This bike sharing demand forecast project made extensive use of the AutoGluon AutoML framework for Tabular Data.
The features of the AutoGluon framework were extensively utilised to create automatic stack ensembled as well as individually different configurable regression models trained on tabular data. It aided in the rapid development of a base-line model.
The top-ranked AutoGluon-based model greatly improved outcomes by using data from intensive exploratory data analysis (EDA) and feature engineering without hyperparameter optimisation.
AutGluon was able to investigate and utilise the best available alternatives by leveraging autonomous hyperparameter tweaking, model selection/ensembling, and architectural search.
Furthermore, hyperparameter optimisation using AutoGluon increased performance over the first raw submission; nonetheless, it was not better than the model with EDA, feature engineering, and no hyperparameter tuning.

