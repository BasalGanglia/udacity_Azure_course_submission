# Optimizing an ML Pipeline in Azure

## Overview
This project is part of the Udacity Azure ML Nanodegree.
In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model.
This model is then compared to an Azure AutoML run.

## Summary
Because the datafile is called bankmarketing_train.csv, we can deduce that the data has something to do with finance. The column we are predicting (the y value, or the dependent variable) based on the provided data cleaning script contains values "yes" and "no".  This is then converted to 1 for yes and 0 for no.

The predictors include wide range of features such as marital status (converted 1/0), whether the person has defaulted, whether they have housing, have loan and so on. 
The predictors also include things like the education level of the participant. 

Some of the variables, such as "contact" (whatever that might be) and "education" are one-hot-encoded using pandas get_dummies method. 
The days and months are converted to numeric values. 

## Scikit-learn Pipeline

For the scikit-learn pipeline, we preprocess the data with steps I described in the summary section. We then use a logistic regression for the binary classification task.
Once the data is cleaned, it is split into testing and training sets. The Logistic regression take in as hyperparamter C which is the inverser of the regularization strength. We also use as hyperparameter the maximum number of iterations. As the scoring metrics we use accuracy

I selected randomparamtersampling to sample the hyperparameters as this is faster than the gridsearch. 

I selected BanditPolicy as the early stopping policy, a it allows me to specify, with the slack-amount parameter, runs that are not good compared to the best run so far.

## AutoML
Best model found by AutoML is actually an Voting Ensemble of the of the best models that uses several models and bases its prediction on the avaraged vote of these models. The model achieved 91.6% accuracy. Looking at the feature importances in Machine Learning Studio, I can see that duration, emp.var.rate and nr.employed were the 3 most important features. Looking at the AutoML get_details() output I can see that the best run had such parameters as n_estimators = 10, min_samples_split=0.1505, n_jobs=1, random_state=None

## Pipeline comparison
We are compare two pipelines, one where a scikit-learn based logistic regression model has its hyperparameters (C and max-iter) tuned by the hyperdrive service, and another pipeline where we use Azure AutoML to automatically compare multiple machine learning models.
The logistic regression achieved around 91.3% accuracy. Considering that we had around 40 features it makes sense that the ensemble method outperformed the basic logistic regression. The voting ensemble only achiveed 91.6% accuracy, so not really substantial improvement over the logistic regression. Howerver, the other metrics, such as AUC weighted (at 0.95755) were nice for the AutoML.

## Future work
Proper feature pre-processing (the current clean_data) would probably help the performance. For example normalizing the features. Also, using some more complicated scikit-learn model, such as random forest or gradient boosting, would probably perform much better than logistic regression. Also, using cross-validation for the scikit-learn model would have been a good idea to reduce over-fitting (AutoML handles cross-validation automatically.)

## Proof of cluster clean up
I did this on my personal Azure account.
The jupyter notebook has output of the deletion operation.

```

```
