---
title: How to Evaluate your Model - EN
tags: ML DL Metrics 
---

# Introduction

## Background

One might think that neural networks are better than decision trees, and decision trees are better than logistic regression. However, it is meaningless to simply compare models since each model has its own applicable scenario. To evaluate the goodness of a model needs to be placed in a specific data scenario. To discuss the issue of how to evaluate the model, we have to start with how the data are handled.

## Handle the Data

The evaluation of the model is to ensure that your model is broadly useful, that is to say that your model should maintain good performance on the dataset used for training as well as on datasets beyond it without under-fitting or over-fitting.

### Data Set Division(Holdout)

Generally, the sample is divided into three separate part: **training set**, **validation set** and **test set**. The training set is used to fit the model. The validation set is used to select the optimal values of tuning parameters (model selection). The test set is used to evaluate the generalization ability of the model. A typical division is that the training set accounts for 50% of the total sample, while the others each account for 25%, and all three parts are randomly selected from the sample. Although such a partitioning approach is simple and flexible, its model performance evaluation is more sensitive to the ratio of the partitioning of the training set and validation set which can result in meaningful differences in the estimate of accuracy.

Usually we will get a data set containing a labeled data set (as the training set) and an unlabeled one (as the test set), then we need to manually divide a validation set from the training set when we train the model. 

```python
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(train_data, train_target, test_size=0.25, random_state=0)
#train_data:feature train_target:label test_size=0.25:25% is test set
```

### Cross-Validation

Cross validation is a technique that involves partitioning the original dataset into a training set, used to train the model, and an validation set used to evaluate the analysis. The most common cross-validation technique is **k-fold cross-validation**, where the original dataset is partitioned into k equal size subsamples, called folds. The k is a user-specified number, usually with 5 or 10 as its preferred value. This is a dynamic verification approach, which can reduce the impact caused by data division. The specific steps are as follows:

1. Divide the data set into a training set and a test set, and put the test set aside
2. Divide the training set into k folds
3. Use 1 of the k folds as the validation set each time while the others are used as the training set. 
4. After k training sessions, we get k different models. 
5. Evaluate the effect of k models and select the best hyperparameters from them.
6. Use the best hyperparameters and then retrain the model with all k data as training set to get the final model.

```python
from sklearn.model_selection import KFold
kf = model_selection.KFold(n_splits=10, random_state=None, shuffle=False)
digits_gen = kf.split(digits.data)
for train_idx, test_idx in digits_gen:
        X_train = digits.data[train_idx] #Training set
        X_test = digits.data[test_idx] #Test set
        y_train = digits.target[train_idx] #Training set label
        y_test = digits.target[test_idx] #Test set label
```



# Model Evaluation Metrics

## Intro

Model evaluation metrics are required to quantify model performance. The choice of evaluation metrics depends on a given machine learning task (such as classification, regression, clustering). Regression models and classification models are two of the most important components of machine learning.

For classification models, we usually use accuracy, confusion matrix, precision, recall, F1 Score, ROC curve, AUC value, etc. to evaluate.

For regression models, we usually use MSE, RMSE, MAE, MAPE, etc. to evaluate.

## Classification Models

### Confusion Matrix, Accuracy, Precision, Recall, F1

[![ge884H.png](https://z3.ax1x.com/2021/05/02/ge884H.png)](https://imgtu.com/i/ge884H)

#### Confusion Matrix

[![ge8XqK.jpg](https://z3.ax1x.com/2021/05/02/ge8XqK.jpg)](https://imgtu.com/i/ge8XqK)

The confusion matrix is an N X N matrix, where N is the number of classifications. If we are dealing with a binary classification problem, i.e. N = 2, we get a 2 X 2 matrix. The confusion matrix can provide a more detailed breakdown of correct and incorrect classifications for each class. 

#### Accuracy

Accuracy is a common evaluation metric for classification problems. It’s the number of correct predictions made as a ratio of all predictions made.


$$
Accuracy = M_{correct} / M_{total}
$$


In binary classification, the accuracy rate can be obtained by the following formula:


$$
Accuracy = (TP+TN) / (TP+TN+FP+FN)
$$


Accuracy is one of the simplest and most intuitive metrics to evaluate in classification problems, but there are some limitations to accuracy. For example, in binary classification, when the percentage of negative samples is 99%, if the model predicts all samples as negative samples, it can also obtain 99% accuracy. Although the accuracy seems to be high, the model is actually useless because it cannot find a single positive sample. When the data is abnormally unbalanced, although the Accuracy Score is high, it is meaningless.

#### Precision

Precision is the ratio of correctly predicted positive observations to the total predicted positive observations.


$$
Precision = TP/(TP+FP)
$$

#### Recall (Sensity)

Recall is the ratio of correctly predicted positive observations to the all observations in actual class.


$$
Recall = TP/(TP+FN)
$$

#### F1 Score

F1 Score is the weighted average of precision and recall. In general, precision and recall are mutually exclusive, that is, if the precision is high, the recall will be low; if the recall is high, the precision will be low. Therefore, F1 score was designed to consider both precision and recall.


$$
F1 = 2*(Recall * Precision) / (Recall + Precision)
$$


F1 score can be generalized to a weighted average of different weights assigned to precision and recall.


$$
F_a = [(1+a^2)*(Recall*Precision)]/[a^2*Precision+Recall]
$$


The magnitude of a indicates the relative importance of recall to precision.

#### Notice

1. Accuracy is not suitable for data sets with unbalanced data.
2. The problem mentioned above is based on a binary classification problem, and the precision and recall rates are binary classification metrics that do not apply to multi-classification.
3. When the cost of False Negative (FN) is high (with serious consequences) and you want to avoid FN as much as possible, you should focus on improving Recall.
4. When the cost of False Positive (FP) is high (with serious consequences) and you want to avoid FP as much as possible, you should focus on improving the Precision.
5. Accuracy can be applied to multiclassification evaluation. A multiclassification problem can be solved by converting it to a binary problem by reducing the class of concern to one class and all other classes to one class.

### ROC&AUC

#### ROC

ROC(Receiver Operation Characteristic Curve)，this curve plotted with the true positive rate as the vertical coordinate and the false positive rate as the horizontal coordinate, which is a composite indicator of the continuous variables of sensitivity and special effects. It is generally believed that the smoother the ROC indicates the lower probability of overfitting of the classification algorithm, and the steeper the ROC is away from the diagonal line and closer to the upper left corner indicates the better classification performance.

In many machine learning models, the output of many models is the prediction probability. When evaluating models using metrics such as precision and recall, it is necessary to set a classification threshold for the prediction probability, such that a prediction probability greater than the threshold is a positive case and the opposite is a negative case. The ROC curve does not need to set such a threshold, and the vertical coordinate of the ROC curve is the true positive rate and the horizontal coordinate is the false positive rate.


$$
[Sensitivity=Recall= Y-axis]True Positive Rate(TPR)= TP /(TP+FN)
$$

$$
[1-Specificity=X-axis]FalsePositiveRate(FPR)=FP/(FP+TN)
$$



When the distribution of positive and negative samples in the test set changes, the ROC curve is able to remain unchanged, ignoring the sample imbalance.

#### AUC

The area under the ROC curve is the AUC value, which can only be used for the evaluation of a binary classification model. The AUC is the probability that given a positive sample and a negative sample at random, if the classifier outputs the positive sample with a greater probability than the negative sample with a positive probability. Therefore, AUC reflects the classifier's ability to rank the samples. The larger the AUC value, the better, ideally 1. Normally it must be at least greater than 0.5 to be meaningful.

#### Notice

1. ROC curves do not make sense in multi-categorization, only when positive and negative are equally important in binary classification, ROC curves are suitable for evaluation.
2. If you really need to use ROC curves in multiclassification problems, you can transform them into multiple "one-to-many" problems. That is, one of them is treated as a positive case and the rest as a negative case, and multiple ROC curves are drawn.

## Regression Models

### MSE&RMSE

#### MSE

MSE (Mean Squared Error) is generally used to detect the deviation between the predicted and true values of a model. MSE is the square of the difference between the true and predicted values and then summed and averaged. The squared form is easy to derive, so it is often used as a loss function in linear regression.


$$
MSE=\frac1m*\sum_{i=1}^m(y_{test}^i-{\hat{y}}_{test}^i)^2
$$

#### RMSE

RMSE (Root Mean Squarde Error) is a square root measure of the deviation between the observed and true values based on MSE. It is often used as a measure of the prediction results of machine learning models.


$$
RMSE = \sqrt[]{\frac1m*\sum_{i=1}^m(y_{test}^i-{\hat{y}_{test}^i})^2} = \sqrt[]{MSE_{test}}
$$

### MAE&MAPE

#### MAE

MAE (Mean Absolute Error) is the average of the absolute error. It can better reflect the actual situation of the prediction value error.


$$
MAE =\frac1m*\sum_{i=1}^m|y_{test}^i-{\hat{y}}_{test}^i|
$$


#### MAPE

MAPE (Mean Absolute Percentage Error) is called Mean Absolute Percentage Error. MAPE of 0% indicates a perfect model, while MAPE greater than 100 % indicates a poor model.


$$
MAPE =\frac{100\%}m*\sum_{i=1}^m|\frac{\hat{y}_{test}^i-y_{test}^i}{y_{test}^i}|
$$

------

**Reference/参考**: 

1. [训练集、验证集、测试集](https://cloud.tencent.com/developer/article/1558428)
2. [如何评估模型好坏](https://www.jianshu.com/p/41f434818ffc)
3. [一份非常全面的机器学习分类与回归算法的评估指标汇总](https://cloud.tencent.com/developer/article/1356921)

