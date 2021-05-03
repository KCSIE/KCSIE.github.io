---
title: How to Evaluate your Model
tags: AI ML DL Notes
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

# 引入

## 背景

可能有人会认为神经网络比决策树要好，决策树比逻辑回归要好。然而，单纯地比较模型是没有意义的，每一个模型都有自己的适用场景。要评估模型的好坏需要放在一个特定的数据场景下。要讨论如何评价模型这个问题，得先从数据的处理说起。

## 数据处理

模型的评估是确保你的模型是广泛有用的，这就是说你的模型要在用于训练的数据集以及这之外的数据集上都能保持较好的准确性，不会出现欠拟合或过拟合的现象。

### 数据集划分

一般需要将样本分成独立的三部分训练集，验证集和测试集。其中训练集用来拟合模型的，验证集用来调参优化（模型选择），而测试集用于评估模型的泛化能力。一个典型的划分是训练集占总样本的50％，而其它各占25％，三部分都是从样本中随机抽取。 尽管这样的划分方式是简单灵活的，它的模型性能评估对训练集和验证集的分割的比例较为敏感，这会导致对准确度的估计出现有意义的差异。

通常我们得到的数据集会包含一个标注的数据集（作为训练集）以及一个没有标注的作为测试集，那么我们训练模型的时候需要人工从训练集中划分一个验证集出来。

```python
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(train_data, train_target, test_size=0.25, random_state=0)
#train_data:feature train_target:label test_size=0.25:25% is test set
```

### 交叉验证

交叉验证是一种将原始数据集划分为训练集（用于训练模型）和验证集（用于评估分析）的技术。最常见的交叉验证技术是**K折交叉验证**，即将原始数据集划分为k个相等大小的子样本称为folds，k是用户指定的数字通常以5或10作为其首选值。这是一种动态验证的方式，这种方式可以降低数据划分带来的影响。具体步骤如下：

1. 将数据集分为训练集和测试集，将测试集放在一边
2. 将训练集分为 k 份
3. 每次使用 k 份中的 1 份作为验证集，其他全部作为训练集。
4. 通过 k 次训练后，我们得到了 k 个不同的模型。
5. 评估 k 个模型的效果，从中挑选效果最好的超参数
6. 使用最优的超参数，然后将 k 份数据全部作为训练集重新训练模型，得到最终模型。

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


# 模型评估指标

## 导览

模型评价指标源于量化模型性能的需要。评价指标的选择取决于特定的机器学习任务（如分类、回归、聚类）。回归模型和分类模型是机器学习的两个最重要的组成部分。

对于分类模型，我们通常使用准确率、混淆矩阵、精确率、召回率、F1值、ROC曲线、AUC值等来评价。

对于回归模型，我们通常使用MSE、RMSE、MAE、MAPE等来评估。

### 混淆矩阵，准确率，精确率，召回率， F1值

[![ge884H.png](https://z3.ax1x.com/2021/05/02/ge884H.png)](https://imgtu.com/i/ge884H)

#### 混淆矩阵

[![ge8XqK.jpg](https://z3.ax1x.com/2021/05/02/ge8XqK.jpg)](https://imgtu.com/i/ge8XqK)

混淆矩阵是一个N X N矩阵，N为分类的个数。假如我们面对的是一个二分类问题，也就是N＝2，我们就得到一个2 X 2矩阵。混淆矩阵可以为每个类别的正确和不正确分类提供更详细的分类。

#### 准确率

准确率是分类问题的一个常见评价指标，它是模型预测正确（包括预测为真正确和预测为假正确）的样本数量占总样本数量的比例。


$$
Accuracy = M_{correct} / M_{total}
$$


在二分类问题中，准确率可以由如下公式表示：


$$
Accuracy = (TP+TN) / (TP+TN+FP+FN)
$$


准确率是分类问题中的一个最简单也最直观的评估指标，但是准确率存在一些局限性。比如，在二分类中，当负样本占比 99 %时，如果模型把所有样本都预测为负样本也能获得 99% 的准确率。虽然准确率看起来很高，但是其实这个模型时没有用，因为它找不出一个正样本。当数据不平衡时，尽管准确率很高，它是没有意义的。

#### 精确率

精确率指模型预测为真，实际也为真的样本数量占模型预测所有为真的样本数量的比例。


$$
Precision = TP/(TP+FP)
$$

#### 召回率 （灵敏度）

召回率是指模型预测为真，实际也为真的样本数量占实际所有为真的样本数量的比例。


$$
Recall = TP/(TP+FN)
$$

#### F1值

F1值是精确度和召回率的调和平均值。一般来说，精确率和召回率是互斥的，也就是说精确率高的话，召回率会变低；召回率高的话，精确率会变低。所以设计了一个同时考虑精确率和召回率的指标 F1值。


$$
F1 = 2*(Recall * Precision) / (Recall + Precision)
$$


F1值可泛化为对精确率和召回率赋不同权值进行加权调和。


$$
F_a = [(1+a^2)*(Recall*Precision)]/[a^2*Precision+Recall]
$$


a的大小表示召回率对精确率的相对重要程度。

#### 注意

1. 准确率不适用于数据不平衡的数据集。
2. 上述问题是基于二分类问题的，精确率和召回率是二分类指标，不适用多分类
3. 当False Negative (FN)的成本代价很高 (后果很严重)，希望尽量避免产生FN时，应该着重考虑提高Recall指标。
4. 当False Positive (FP)的成本代价很高 (后果很严重)时，即期望尽量避免产生FP时，应该着重考虑提高Precision指标。
5. 准确率适用于多分类评估。可以将多分类问题转换为二分类问题进行求解，将关注的类化为一类，其他所有类化为一类。

### ROC曲线与AUC值

#### ROC曲线

ROC，受试者工作特征曲线，以真阳性率为纵坐标，假阳性率为横坐标绘制的曲线，是反映灵敏性和特效性连续变量的综合指标。一般认为ROC越光滑说明分类算法过拟合的概率越低，ROC越远离对角线，越陡峭，越接近左上角说明分类性能越好。

在众多的机器学习模型中，很多模型输出的是预测概率，而使用精确率、召回率这类指标进行模型评估时，还需要对预测概率设分类阈值，比如预测概率大于阈值为正例，反之为负例。这使得模型多了一个超参数，并且这超参数会影响模型的泛化能力。ROC曲线不需要设定这样的阈值，ROC曲线纵坐标是真正率，横坐标是假正率。


$$
[Sensitivity=Recall= Y-axis]True Positive Rate(TPR)= TP /(TP+FN)
$$

$$
[1-Specificity=X-axis]FalsePositiveRate(FPR)=FP/(FP+TN)
$$



当测试集中的正负样本的分布变化的时候，ROC曲线能够保持不变，无视样本不平衡。

#### AUC值

ROC曲线下的面积即AUC值，只能用于二分类模型的评价。AUC是指随机给定一个正样本和一个负样本，分类器输出该正样本为正的那个概率值比分类器输出该负样本为正的那个概率值要大的可能性，所以AUC反应的是分类器对样本的排序能力。AUC值越大越好，理想情况是1，其余情况至少要大于0.5才有意义。

#### 注意

1. ROC曲线用在多分类中是没有意义的，只有在二分类中Positive和Negative同等重要时候，适合用ROC曲线评价。
2. 如果确实需要在多分类问题中用ROC曲线的话，可以转化为多个“一对多”的问题。即把其中一个当作正例，其余当作负例来看待，画出多个ROC曲线。

## 回归模型

### MSE&RMSE

#### MSE

MSE(Mean Squared Error)叫做均方误差，一般用来检测模型的预测值和真实值之间的偏差。MSE是真实值与预测值的差值的平方然后求和平均。通过平方的形式便于求导，所以常被用作线性回归的损失函数。


$$
MSE=\frac1m*\sum_{i=1}^m(y_{test}^i-{\hat{y}}_{test}^i)^2
$$

#### RMSE

RMSE(Root Mean Squarde Error)叫做均方根误差，是在MSE的基础上做平方根衡量观测值与真实值之间的偏差，常用来作为机器学习模型预测结果衡量的标准。


$$
RMSE = \sqrt[]{\frac1m*\sum_{i=1}^m(y_{test}^i-{\hat{y}_{test}^i})^2} = \sqrt[]{MSE_{test}}
$$

### MAE&MAPE

#### MAE

MAE(Mean Absolute Error)叫做平均绝对误差，是绝对误差的平均值。它可以更好地反映预测值误差的实际情况。


$$
MAE =\frac1m*\sum_{i=1}^m|y_{test}^i-{\hat{y}}_{test}^i|
$$


#### MAPE

MAPE(Mean Absolute Percentage Error)叫做平均绝对百分比误差。MAPE 为0%表示完美模型，MAPE 大于 100 %则表示劣质模型。


$$
MAPE =\frac{100\%}m*\sum_{i=1}^m|\frac{\hat{y}_{test}^i-y_{test}^i}{y_{test}^i}|
$$



**Reference/参考**: 

https://cloud.tencent.com/developer/article/1558428

https://www.jianshu.com/p/41f434818ffc

https://cloud.tencent.com/developer/article/1356921

