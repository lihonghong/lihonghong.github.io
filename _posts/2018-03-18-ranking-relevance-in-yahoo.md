---
title: "Ranking Relevance in Yahoo Search"
date: 2018-03-18
comments: true
categories:  search
tags: ranking
keywords: learning to rank; query rewriting; semantic matching; deep learning

---

## 要点
1. 提出新的排序算法
2. 开发语义特征
3. 利用query改写扩召回
4. 提出时效性排序和位置敏感性排序方案

## 排序
排序过程分为三步：base ranking -> core ranking ->contextual reranking.  
1. 第一步为粗排序，使用轻量级模型.  
2. 第二步使用ltr，论文提出了LogisticRank，实验数据给出结果是优于GBRank、LambdaMart，理由是真实样本好结果分布较少.    
3. 第三步基于全部返回结果进行重排序.

## 语义特征
1. Click Similarity
2. Translated Text Matching
3. Deep Semantic Matching

## query改写
1. The Learning Phase
2. The Decoding Phase  

![avatar](/images/latex/query_rewrite.png)

## 时效性、位置排序
![avatar](/images/latex/time_rank.png)  
c(x)为时效性分类器，当query-url预测为时效性时，在相关性模型基础上加入时效性r(x)
![avatar](/images/latex/poi_rank.png)
结合基础排序函数f(x)、距离函数d(query,url)，构造pierwise排序模型
## 论文
[Ranking Relevance in Yahoo Search](http://www.kdd.org/kdd2016/subtopic/view/ranking-relevance-in-yahoo-search)
