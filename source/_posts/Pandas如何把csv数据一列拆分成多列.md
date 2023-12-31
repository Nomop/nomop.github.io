---
title: Pandas如何把csv数据一列拆分成多列
date: 2023-11-21 18:06:19
tags: [机器学习,数据处理,Pandas]
categories: MachineLearning
description: 解决网上下载的csv数据集只集中在一列的情况，得到一个多列特征的df对象
---

## 问题

有时候网上下载下来的CSV不是那种规整的每一行一个数据，每一列一个特征，而是全部堆在第一列
像这样
![](https://vip.helloimg.com/images/2023/11/21/owQv5Y.png)

如果你直接读出来成为DataFrame对象，就会变成这样
【n rows X 1 columns】
![](https://vip.helloimg.com/images/2023/11/21/owQ0vX.png)

## 解决方法

在使用pd读取csv文件时，使用**sep参数**来指定CSV文件中字段之间的分隔符。

分割符一般是逗号','或者制表符'\t'。我这里以用';'作为分割符，具体代码如下

```Python
import pandas as pd
df = pd.read_csv('数据分析3数据\winequality.csv',sep='\;',encoding='gb18030')
print(df)
```
![运行结果](https://vip.helloimg.com/images/2023/11/21/owQws9.png)

你眼睛👀尖一点就会发现我这里的分隔符是'\;'但是这也能成功运行
我第一使用';'没能成功，然后加了一个'\'就成功了······
然后后面就这两个都能用，如果你的分隔符没有发挥作用，可以试一试加一个'\'

## 总结

最开始我想着傻傻地把读进来的df用像字符串处理列表，像是


```
df.iloc.str.split(';')
```
当时脑子里是想用这种方法来把第一行字符串和每一行数据都用“;”分隔，对第一行字符串里的多个特征名按照分隔符提取多个列，作为新的列，然后每一行数据中多个数据按照分隔符提取，按照和特征名一样的次序分配到对应的列中，巴拉巴拉一大堆费事又头疼的字符串处理，现在想想还是很好笑的。

最后发现有参数可以在读取的时候直接完成处理，心情又开心又难受

一方面是自己不够熟悉方法函数，上课也没认真听，不知道的东西你怎么用？
另一方面是没有原则地浪费时间，如果什么小的功能你不能自己快速简单的实现，别人肯定已经帮你写好了！不要再造轮子了！赶紧STFW!

参考资料：
https://zhuanlan.zhihu.com/p/129004421