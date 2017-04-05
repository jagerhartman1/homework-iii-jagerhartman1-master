# homework-iii-starter
the starter repository for hw3

## Team Type III Error:
* Jager Hartman (jwh2163)
* Moorissa Tjokro (mmt2167)

## Task
<p>A banking institution ran a direct marketing campaign based on phone calls. Often, more than one contact to the same client was required, in order to assess if the product (bank term deposit) would be subscribed or not. Your task is to predict whether someone will subscribe to the term deposit or not based on the given information.</p>

## Classification Technique Overview

<p>Our original approach was to create a simple poor man's stacking ensemble with models that were somewhat simplistic. We first tried stacking NaiveBayes, RandomForest, ExtraTreeClassifier, SVM and logistic regression together. These models performed well with regards to cross validation and on the testing set with roc-auc scores around 0.78-0.8. However, when submitting the Kaggle the score dropped to 0.76. Gaussian Naive Bayes was one of the strongest performers though did not add anything to the ensemble methods. As an aside, we tried NearestCentroid and KNN though had issues with consistent predict_proba calls so dropped these models as well.</p>

<p>*Note that all model hyperparameters were tuned using GridSearch with cv=5. Not all grid searches are included due to time in execution of the notebook.</p>

<p>Moving forward we decided to drop the SVM all together due to time constraints and drop NaiveBayes since it was performing strangely. We were then left with gradient boosting, ada boosting, easy ensembles, random forests and logistic regression with feature selection. The ExtraTree classifier was left out since the random forests would be more powerful and pick up on similar trends. AdaBoosting overfit too much and dominated the stacking ensemble. The gradient boost also overfit quite a lot but there seemed to be an improvement in the Kaggle scores when using this model. Cross-validation and the test set showed roc-auc's around 0.8 - 0.82 with the ensemble methods implementing the gradient boosted random forest. This left us with Gradient Boosting random forests and different implementations of logistic regression such as AdaBoost, easy ensemble and other sampling techniques.</p>

<p>The feature selection showed little imrpovements applied to all of the data prior to the voting classifier for poor-man's stacking. This was due to the tree models we were using. Instead, applying an RFE(RandomForest()) selector prior to logistic regression alone seemed to perform the best.</p>

<p>Standard scaling and min-max scaling seemed to perform similarly with standard scaling having a slight edge. This is contrary to our belief since the binary data from the dummy variables is between 0 and 1 where the standard scaler would shift the 0's to negative values.</p>

<p>Again, contrary to our belief, SMOTE and omitting a technique to deal with imbalance performed much better than using RandomUnderSampler. Using SMOTE(ratio = 0.5) followed by RandomUnderSampler seemed to give a compromise between the performance of SMOTE alone and RandomUnderSampler alone though showed no improvement over SMOTE alone. This was gauged with regard to logistic regression and the poor-man's stacking classifier.</p>

<p>Another approach we tried was to create an easy ensemble out of the voting classifiers which overfitted, though not as bad as adaboosting, and the results seemed to stay consistent regardless of the number of classifiers used. A further analysis of the affect of number of classifiers on easy ensemble is included at the very end in the analysis of resampling techniques.</p>


