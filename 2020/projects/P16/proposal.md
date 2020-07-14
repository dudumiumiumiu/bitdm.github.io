---
layout: page
mathjax: true
permalink: /2020/projects/p16/proposal/
---

## Covid-19 全球性预测

### 成员

* 杜建成（3220190786）
* 聂宇翔（1120161722）
* 陈子康（3220190783）
* 赵菊文（3220191000）
* 窦京伟（3120190314）

### 问题描述

#### 1、问题背景分析
　　
白宫科学技术政策办公室（OSTP）召集了一个联盟研究小组和公司（包括Kaggle）来准备COVID-19开放研究数据集（CORD-19），以尝试解决有关COVID-19的关键开放科学问题。这些问题来自美国国家科学，工程和医学研究院（NASEM）和世界卫生组织（WHO）。

Kaggle正在发起COVID-19预测挑战，以帮助回答NASEM / WHO问题的一部分。尽管面临的挑战是为每个地区确定5月12日至6月7日之间确诊病例和死亡人数的分位数估计间隔，但主要目标不仅是产生准确的预测。还可以识别出可能影响COVID-19传输速率的因素。

上述挑战是一个回归分析问题。我们组所采用的数据集是Kaggle中COVID19 Global Forecasting (Week 5)任务的数据集。我们通过构建不同的模型并对比分析不同模型在这些数据集上的优劣的方式，对COVID-19未来在世界范围内的传播趋势进行分析。

#### 2、问题描述

2.1 数据准备

采集数据集中的数据，将区域（如全美国）分成适当的$n*n$（如20*20）的数量级的小数据集，然后在每个小区域集上又根据时间统计各个时间段的确诊病例和死亡人数，最后可以得到根据时间段和区域统计的数据统计，完成初步的数据准备。

2.2 准备采用的方法或模型

1. 使用XGBOOST对训练集进行训练，在测试集上对该地区新冠肺炎确认人数和死亡人数进行预测
2. 使用RandomForest对训练集进行训练，在测试集上对该地区新冠肺炎确认人数和死亡人数进行预测
3. 使用logistic regression对训练集进行训练，在测试集上对该地区新冠肺炎确认人数和死亡人数进行预测

2.3 预期的挖掘结果

通过所构建的模型实现对未来COVID-19在确诊人数和死亡人数上较为准确的预测。

### 项目评估

　　预测结果主要利用加权Pinball Loss指标，对各个模型在测试数据集上的性能进行评估。加权Pinball Loss的定义如下所示：

$$
\text{score} = \frac{1}{N_{f}} \sum_{f} w_{f} \frac{1}{N_{\tau}} \sum_{\tau} L_{\tau}(y_i,\hat{y}_{i})
$$

其中，

$$
\begin{eqnarray}
L_{\tau}(y,\hat{y}) & = & (y - \hat{y}) \tau & \textrm{ if } y \geq \hat{y} \\
& = & (\hat{y} - y) (1 - \tau) & \textrm{ if } \hat{y} > y
\end{eqnarray}
$$

并且有，$y$是真实值，$\hat{y}$是预测值，$\tau$是需要被预测的分位数，$N_f$是总的预测数，$N_{\tau}$是总的需要被预测的分位数，$w$是权重因子。

### 项目分工

* 杜建成：模型构建，模型相关部分文档撰写
* 聂宇翔：模型间对比分析，数据可视化，主要文档撰写
* 陈子康：模型构建，模型相关部分文档撰写
* 赵菊文：模型构建，模型相关部分文档撰写
* 窦京伟：数据收集与预处理，以及相关部分文档撰写