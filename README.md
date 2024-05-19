# HR Analytics Predicting Employee Turnover

The main goal of this project is to develop a machine learning model to predict whether an employee will leave the company. A successful model will identify reasons that drive employee turnover.

## Tools Used
* Programming Language: **Python**
* Data Science Libraries/Packages: **pandas, numpy, matplotlib, seaborn, scipy, scikit-learn, xgboost**
* Statistical Methods: **Descriptive statistics, Chi-aquare goodness of fit test**
* Machine learning algorithms: **Decision tree, Random forest, Gradient boosting (XGBoost)**

## Dataset Used

This project used the dataset [Hr Analytics Job Prediction](https://www.kaggle.com/datasets/mfaisalqureshi/hr-analytics-and-job-prediction?select=HR_comma_sep.csv) on Kaggle. The dataset contains data of employees who worked for the company.

## Jupyter Notebook

Ful details of the analysis and model development is available in the provided [Jupyter Notebook]().

## Project Background

A certain company is experiencing high employee turnover - employees leaving the company. As competent and productive employees are indispensable to business growth, companies invest a lot of resources into recruiting, interviewing, and training employees. To improve employee retention, the human resources department collected data about the employees and asked the data analytics team to better understand the data.

## Objectives

The goal of this project is to predict a machine learning model that predicts whether an employee will leave the company. A thorough analysis of the data and an accurate predictive model will answer the following research questions:
1. What types of employees leave the company?
2. Why do employees leave the company?
3. What variables have the most impact on employee turnover?

## Exploratory Data Analysis

The dataset contains 14999 entries of employee data with their reported satisfaction level, last evaluation score, and other work-related data. Employees who left were found to cluster into two groups:
* Group A - These employees tend to work shorter hours, have slightly low satisfaction levels [(see Figure 1)](#figure-1) and low evaluation scores [(see Figure 2)](#figure-2).
* Group B - These employees tend to work the longest hours, have very low satisfaction levels [(see Figure 1)](#figure-1) and very high evaluation scores [(see Figure 2)](#figure-2).

|[Figure 1]()
### Figure 1
Scatter plot of satisfaction level by average monthly hours. The red reference line represents normal working hours of a regular full-time employee.

|[Figure 2]()
### Figure 2
Scatter plot of last evaluation score by average monthly hours. The red reference line represents normal working hours of a regular full-time employee.

The median working hours of employees who left and are working on 2 projects are consistent with Group A as shown in [Figure 3](#figure-3). These employees are likely fired for unsatisfactory performance and were given less work since they were on their way out. On the other hand, employees working on at least 4 projects who left the company have median monthly working hours consistent with Group B. These employees probably quit their job due to overwork.

|[Figure 3]()
### Figure 3
Bar chart of median average monthly hours by number of projects. The red reference line represents normal working hours of a regular full-time employee.

Analysis of satisfaction levels by tenure shows that four-year tenured employees have unusually low satisfaction levels consistent with that of Group B as shown in [Figure 4](#figure-4). Also, none of the long tenured (7 years+) employees left the company.

![Figure 4()
### Figure 4
Bar chart of satisfaction levels by tenure.

Finally, only 1.7% of employees received promotion within the last 5 years, with most employees who worked the longest hours not getting promoted. These observations point to overworking as a major driver of employee turnover.

## Machine Learning Model Development

As satisfaction level may not be available upon deployment of the predictive model, it will not be included in the features for model development. The working hours of Group A are likely set by the management to be lower as they were already identified to be fired, so there is no point in predicting if these employees will leave or not. Instead, the focus of the prediction should be on the ones that will quit their job, which is associated with being overworked. A cut-off value for overwork was set to 177.08 hours, which is the average monthly working hours of an employee who works one hour of overtime for at least 50% of working days.

An XGBoost classifier model was selected to be evaluated on test data as it performed the best out of the models tested. The resulting model performed very well on test data, with evaluation metrics listed below. The model has a balance performance on false positives and negatives; moreover, the model has higher scores on test data than validation data, suggesting that the model does not overfit.

| Metric | Score |
| ------ | ----- |
| Accuracy | 0.967 |
| Precision | 0.900 |
| Recall | 0.902 |
| F1 | 0.901 |
| ROC AUC | 0.941 |

### Table 1
Evaluation scores of the classification model.

The feature importance chart of the model shown in [Figure 5](#figure-5) shows that `tenure_years` has the highest importance, which may possibly be influenced by outliers, where none of the long-tenured (`tenure_years` >= 7) employees left the company.  The next two most important features are related to workload - `number_project` and `overworked`. This confirms that overworking is one of the main factors that drive employee turnover. The fourth most important feature is `last_evaluation`. Earlier EDA showed some positive correlation between `average_number_hours` and `last_evaluation`, suggesting employees that work longer hours tend to have higher evaluation scores.


[Figure 5]()
### Figure 5
Bar chart of the top 10 most important features.

## Conclusion

Insights from exploratory data analysis and feature importances of the machine learning model confirm that employees are overworked. Woking long hours and contributing to several projects without receiving promotion is a characteristic of poor work culture. 

The following actions are recommended to help improve employee retention.
1. Limit the number of projects that employees need to work on.
2. Review policies regarding overtime work. Do not require employees to work overtime or give adequate compensation for overtime work.
3. Consider promoting employees with very high evaluation scores.
4. Review evaluation criteria for employees. In particular, revise evaluation rubrics so that evaluation scores are not largely influenced by working hours.
5. Conduct further investigation into why four-year tenured employees who left tend to have very low satisfaction levels.
influenced by working hours.
5. Conduct further investigation on why four-year tenured employees who left tend to have very low satisfaction levels.