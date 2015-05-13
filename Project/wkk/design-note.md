# wkk 设计笔记

经过一段时间的调研，终于确定了核心系统的设计，这里记录一下，开发时迷失了可以看。

<!-- MarkdownTOC -->

- 系统概述
- 相关技术选择
- 实现流程
- 可能问题

<!-- /MarkdownTOC -->


## 系统概述

知识树是核心，加上文本分类与推荐系统(不一定能做的完)

从ssco中抽取部分本体作为初始网络，网络分为四层：

1. 总分类(Root)
2. 领域大类(父概念只有总分类，属于二级概念)
3. 过渡类(父概念只有总分类以及领域大类，在这一层之下就没有树状结构了)
4. 本体类(父概念为2类或者3类，这一层会有各种的父子概念交叉，弱化层级结构)

其中 123类为具体需要分类的候选，而本体类作为知识推理和逻辑推断的元素，现在利用关键词匹配进行推理和概率传递，通过兄弟节点和父节点的传递来进行概率累积，最终判断属于哪个类别。利用 tag。不能确定的归入总分类，让用户自行判断

进行推荐的时候，同样是根据关键词匹配，来进行具体的推荐，来给出同层级书籍和上一层的书籍推荐，并给出具体的推荐理由

所以这里就要标注数据了，例如哪本书属于哪一些节点，然后每个节点有哪些单词，用来进行匹配和对比

## 相关技术选择

+ tag 是一种简单有效的方法
+ 知识树相当于基因编码(User Profile，根据用户的笔记可以进行倾向性训练)
+ 协同过滤不可用，因为是个人应用
+ 混合推荐与分类(知识树、概率模型、信息提取多种方式都做，来进行比较的选取)
+ 词袋模型+隐含主题模型(topic modeling)
+ 笔记元描述的项目(关键词、分类等等)
+ 同义词的统一
+ 停用词
+ SVM 或者 Naive Bayes
+ 结果评估 Recall, Precision, F-Measure
+ TFIDF
+ 基于图算法的分类

## 实现流程

+ 知识图谱(ssco的子集)
+


## 可能问题

+ 冷启动问题(节点，笔记，书籍)
+ 对于一些冷门物品的推荐
+ 数据稀疏问题
+ 扩展性问题