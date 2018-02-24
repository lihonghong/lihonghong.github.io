---
title: "2017数据挖掘面试问题"
excerpt: 知乎、网易、一点资讯、阿里土豆及摩拜单车的数据挖掘岗面试问题
date: 2017-04-22
comments: true
categories: 面试
tags: [数据挖掘, 面试]
keywords: 数据挖掘, 面试

---

年后去了几家公司面试，攒了些面试经验，以下为一些比较关键的问题整理：

### 知乎
1. map reduce找二度好友(笛卡尔积，一轮解决)
2. LR模型推导，随机森林原理(两个随机，偏差方差)，adaboost原理
3. 求数组最大数，该数为数组中某两个数相加（可以有负）
<!-- more -->
4. 随机器p的概率为0，1-p的概率为0，要求生成0.5的概率为0，0.5的概率为1
5. 给定一个旋转数组，查找某数(二分查找)
6. 之前做的好友推荐使用的特征、模型
7. lucene中，多个搜索结果的倒排链表的合并（交并差等集合操作）

#### 三轮面试的程序题分别为：
1. 求数组最大数，该数为数组中某两个数相加（可以有负）
2. 旋转数组二分查找某数
3. 判断可能有环的两个链表是否相交？(要分三种情况：a、两个都无环。b、两个都有环。c、一个有，一个没有。)

### 网易
程序题，分层打印树？(使用队列)

### 一点资讯
写程序，读写超大文件，并返回文件中第二列字段的值。(开放题，可以上网搜，应该用BufferedReader解决)

### 优酷土豆
程序题，查找数组中有序数字的目标数字的开始和结束位置，例如1，2，3，3，3，5中3的位置为2，4(二分查找)

### 摩拜单车
上来先做笔试题：1、斐波那契数列。2、在字符串中找出连续最长的数字串。3、链表反转。4、最短摘要生成（编程之美上有）