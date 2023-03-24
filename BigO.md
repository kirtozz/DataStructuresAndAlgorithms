## 用大O记法来优化代码

#### 什么是大O记法？

_衡量算法效率的主要指标就是算法需要的步骤数。_

><font size="2">不过，不能简单地说一个算法是“22步的算法”或者“400步的算法”。如果数组有800个元素，那么线性查找就需要800步，明明是解决同类型问题，但算法的步骤数随数据量变化而变化，这明显不是很合适。</font>

 _量化线性查找效率更有效的方法，就是说它**查找数组中的N个元素需要N步**_。

 为了让时间复杂度的讨论更简单，计算机科学家从数学世界里借用了一个概念，这个概念就是大O记法。这种正式表述让我们考研轻松地把算法按照效率分门别类，并与人交流。

 _在最坏的情况下，数组中有多少元素，线性查找就需要多少步。正如先前所述：对于有N个元素的数组，线性查找最多需要N步，用大O记法来表示就是：O(N)，读作“ON”或者“N阶”。_

这个记法表述了一个**核心问题**的答案，这个核心问题就是：__如果有N个数据元素，那么算法需要需要多少步？__

- 特殊的两种时间复杂度

>**<font size="2">时间复杂度O(N)的算法也被称为 *线性时间算法*。 
>时间复杂度O(1)的算法被称作 *常数时间算法*。（无论N是多少，O(1)算法的步骤数都是固定的）**</font>

![BigO1.png](/pictures/BigO1.png "不同复杂度算法的巨大差异")

---
#### 用大O给代码提速

- [冒泡排序](https://github.com/kirtozz/DataStructuresAndAlgorithms/blob/master/SummaryOfAlgorithms.md)


- [选择排序](https://github.com/kirtozz/DataStructuresAndAlgorithms/blob/master/SummaryOfAlgorithms.md)


- [插入排序](https://github.com/kirtozz/DataStructuresAndAlgorithms/blob/master/SummaryOfAlgorithms.md)



 
