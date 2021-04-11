---
title: Brief Introduction to ML
tags: AI ML DL Notes
---

# Learning Map

Machine learning falls into four main categories:

+ Classical Learning
+ Reinforcement Learning
+ Neural Nets & Deep Learning
+ Ensemble Methods

Here's the map:

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/11/04/BgQO58.png" alt="" />



<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/11/04/BgQLUf.png" alt="" />

# 学习导图

机器学习可以分为四类：

+ 经典学习
+ 增强学习
+ 神经网络与深度学习
+ 集成学习

这是导图：

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/11/04/BgQO58.png" alt="" />



<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/11/04/BgQLUf.png" alt="" />

# Machine Learning Process

Terminologies：

- **Model**
  A model is a specific representation learned from data by applying some machine learning algorithm. A model is also called hypothesis.
- **Feature**
  A feature is an individual measurable property of our data. A set of numeric features can be conveniently described by a feature vector. Feature vectors are fed as input to the model. For example, in order to predict a fruit, there may be features like color, smell, taste, etc.
  **Note:** Choosing informative, discriminating and independent features is a crucial step for effective algorithms. We generally employ a feature extractor to extract the relevant features from the raw data.
- **Target (Label)**
  A target variable or label is the value to be predicted by our model. For the fruit example discussed in the features section, the label with each set of input would be the name of the fruit like apple, orange, banana, etc.
- **Training**
  The idea is to give a set of inputs(features) and it’s expected outputs(labels), so after training, we will have a model (hypothesis) that will then map new data to one of the categories trained on.
- **Prediction**
  Once our model is ready, it can be fed a set of inputs to which it will provide a predicted output(label).

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/11/04/BgwCqO.png" alt="" />

Steps:

1. Data collection
2. Data preparation
3. Select a model
4. Ttrain
5. Evaluate
6. Parameter adjustment
7. Forecasting (start of use)

# 机器学习流程

术语：

- **模型**
  模型是通过应用某些机器学习算法从数据中学习的一种特定表示形式。模型也称为假设。
- **特征**
  特征是我们数据的单个可测量属性。可以通过特征向量方便地描述一组数字特征。将特征向量作为模型的输入。例如，为了预测水果，可能会有诸如颜色，气味，味道等特征。
  **注意：**选择信息量大，具有区别性和独立性的特征是有效算法的关键步骤。我们通常使用特征提取器从原始数据中提取相关特征。
- **目标（标签）**
  目标变量或标签是我们的模型要预测的值。对于功能部分中讨论的水果示例，带有每组输入的标签将是水果的名称，例如苹果，橙子，香蕉等。
- **训练**
  想法是给出一组输入（特征）和预期的输出（标签），因此在训练之后，我们将得到一个模型（假设），该模型将新数据映射到一个训练过的类别中。
- **预测**
  一旦我们的模型准备好了，就可以向它提供一组输入，它将提供预测的输出（标签）。

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/11/04/BgwCqO.png" alt="" />

步骤：

1. 收集数据
2. 数据准备
3. 选择一个模型
4. 训练
5. 评估
6. 参数调整
7. 预测（开始使用）

# Classical Learning

Classical machine learning is often divided into two categories: supervised learning and unsupervised learning(In fact, there's semi-supervised learning between them):

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/11/04/BgQqVP.png" alt="" />



## Supervised Learning

The computer is presented with example inputs and their desired outputs, given by a “teacher”, and the goal is to learn a general rule that maps inputs to outputs. The training process continues until the model achieves the desired level of accuracy on the training data.

Here's some supervised learning methods:

+ Regression
  + Linear Regression
  + Logistic Regression(Used as classifier)
+ Classifition
  + Distance-based algorithms
  + Naive Bayes
  + Decision Trees
  + Support Vector Machine(SVM)
  + K-NearestNeighbor(K-NN)

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/11/04/Bgaapq.png" alt="" />

## Unsupervised learning

No labels are given to the learning algorithm, leaving it on its own to find structure in its input. It is used for clustering population in different groups. Unsupervised learning can be a goal in itself (discovering hidden patterns in data).

Here's some unsupervised learning methods:

+ Clustering
  + K-means
  + Spectral clustering
+ Dimension Reduction(Generalization)
  + Singular Value Decomposition(SVD)
  + Latent Semantic Analysis(LSA)
+ Representation Learning

## Semi-supervised learning

Problems where you have a large amount of input data and only some of the data is labeled, are called semi-supervised learning problems. These problems sit in between both supervised and unsupervised learning.

## Difference Between Supervised Learning & Unsupervised learning

| Supervised Learning      | Unsupervised learning          |
| ------------------------ | ------------------------------ |
| Target(Label) is clear   | Target(Label) is unclear       |
| Need data set with label | Don't need data set with label |
| Easy to evaluate         | Hard to evaluate               |

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/11/04/BgdYDO.png" alt="" />

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/11/04/BgdB8I.png" alt="" />

# 经典学习

经典的机器学习方法常被分为两类：监督学习和无监督学习(事实上，这两个间还有半监督学习):

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/11/04/BgQqVP.png" alt="" />



## 监督学习

计算机会收到一个 "老师 "给出的输入示例及其期望的输出，目标是学习一个将输入映射到输出的一般规则。训练过程继续进行，直到模型在训练数据上达到预期的准确度。

这是几种监督学习方法：

+ 回归
  + 线性回归
  + 逻辑回归(本质是线性回归，但用作分类的分类器)
+ 分类
  + 基于距离的算法
  + 朴素的贝叶斯算法
  + 决策树
  + 支持向量机(SVM)
  + K最邻近算法(K-NN)

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/11/04/Bgaapq.png" alt="" />

## 无监督学习

不给学习算法任何标签，让它自己去寻找输入中的结构。它用于在不同的群体中对人群进行聚类。无监督学习本身就可以成为一个目标（发现数据中的隐藏模式）。

这是一些无监督学习方法：

+ 聚类
  + K均值算法
  + 谱聚类
+ 降维
  + 奇异值分解(SVD)
  + 隐形语义3分析(LSA)
+ 表征学习

## 半监督学习

如果你有大量的输入数据，但只有部分数据被标记，这些问题被称为半监督学习问题。这些问题介于监督学习和无监督学习之间。

## 监督学习与无监督学习的区别

| 监督学习           | 无监督学习           |
| ------------------ | -------------------- |
| 目标明确           | 目标不明确           |
| 需要带标签的数据集 | 不需要带标签的数据集 |
| 效果易于评估       | 效果难以评估         |

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/11/04/BgdYDO.png" alt="" />

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/11/04/BgdB8I.png" alt="" />

# Reinforcement Learning

A computer program interacts with a dynamic environment in which it must perform a certain goal (such as driving a vehicle or playing a game against an opponent). The program is provided feedback in terms of rewards and punishments as it navigates its problem space.

+ Agent-oriented learning—learning by interacting with an environment to achieve a goal
+ Learning by trial and error, with only delayed evaluative feedback (reward)
+ Trade-off between exploration and exploitation

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/11/04/BgBSHO.png" alt="" />

# 增强学习

一个计算机程序与一个动态环境互动，在这个环境中，它必须完成某个目标（如驾驶车辆或与对手玩游戏）。当程序在其问题空间中导航时，它将得到奖惩方面的反馈。

+ 面向代理的学习--通过与环境互动来实现目标的学习。

+ 通过试错学习，仅有延迟的评价性反馈(奖励)
+ 探索与开发之间的权衡

<img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/11/04/BgB8vq.jpg" alt="" />

# Ensemble Methods

The ensemble methods refers to combining multiple models in order to get better results and to make the integrated models more generalizable. For multiple models, there are several different thoughts on how to combine these models:

+ Finding the best performing model on the validation dataset as the final predictive model
+ Voting or averaging the predictions of multiple models
+ A weighted average of the predictions from multiple models

Here's the three methods:

+ Stacking

  <img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/11/04/Bgc4JS.png" alt="" />

+ Bagging

  <img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/11/04/Bgc5Rg.png" alt="" />

+ Boosting

  <img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/11/04/Bgchi8.png" alt="" />

# 集成方法

集成学习方法是指组合多个模型，以获得更好的效果，使集成的模型具有更强的泛化能力。对于多个模型，如何组合这些模型，主要有以下几种不同的思路：

+ 在验证数据集上上找到表现最好的模型作为最终的预测模型
+ 对多个模型的预测结果进行投票或者取平均值

+ 对多个模型的预测结果做加权平均

这是三种主要方法：

+ Stacking

  <img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/11/04/Bgc4JS.png" alt="" />

+ Bagging

  <img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/11/04/Bgc5Rg.png" alt="" />

+ Boosting

  <img style="display: block; margin: 0 auto;" src="https://s1.ax1x.com/2020/11/04/Bgchi8.png" alt="" />



**Reference/参考：**

https://vas3k.com/blog/machine_learning/

https://www.geeksforgeeks.org/

<img style="display: block; margin: 0 auto;" src="" alt="" />