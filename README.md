# Optimizing an ML Pipeline in Azure

## Overview
This project is part of the Udacity Azure ML Nanodegree.
In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model.
This model is then compared to an Azure AutoML run.

## Summary
Nowhere in the project description was there any explanation what this data is, so I have to make an educated guess based on the column names and the file name (something that would never happen in real datascience project...). Because the datafile is called bankmarketing_train.csv, we can deduce that the data has something to do with finance. The column we are predicting based on the provided data cleaning script seems to contain values "yes" and "no". What these means is impossible to determine, so I'll just handle this as a binary classification problem where we are predicting something unknown based on random features. 

Because we are dealing with a binary classification problem, a natural idea is to use logistic regression, which was done here.

## Scikit-learn Pipeline
I followed the project instructions, so there was no real pipelinehere. The features were not scaled or centered or anything such, they were just fed directly into the logistic regression (after of course being converted to numeric values from strings).

I chose the randomparametersampling because it was pretty much the only only option, there are no real benefits for it over gridsearch except maybe it is slightly faster.

In theory the early stopping might make the runs go faster. In this artificial experiment it was just waste of time to implement.

## AutoML
The autoML generated something called VotingEnsemble (according to the Azure ML Studio GUI), so apparently somekind of ensemble method performed best, achieving over 95% accuracy  (weighted_accuracy 0.9538785580226481, AUC_macro 0.9430183393274798.
norm_macro_recall 0.5266777897652332)
## Pipeline comparison
The logistic regression achieved around 90.8% accuracy. Considering that we had around 40 features it makes sense that the ensemble method outperformed the basic logistic regression.

## Future work
Feature preprocessing might help the performance, because that is why it is done...

## Proof of cluster clean up
I did this on my personal Azure account.


```

```
