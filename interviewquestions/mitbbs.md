mitbbs

8. [facebook] 给一个N个node的BST，给一个key，返回与key最接近的m个node(m < N)。
中序遍历加队列

9. [facebook] 用一个数组来表示二维数组，但是每一行的元素个数可以不同，实现get, set函数。
①按列存
②按行存
③hash, i, j, val组成key

12. [google] 两个不知长度的int数组，实现相加。
模拟

15. [google] Boggle game。从一个字符开始找邻居字符然后继续找，形成一个word。条件是，形成了word之后要继续找，因为可能有更长的word。一旦用了一个字符以后，就不可以重复使用了。
深搜



20. 说一个大楼,10层,4个电梯,怎么设计类来实现这样一个系统? 
http://www.mitbbs.com/article_t/JobHunting/31376671.html
amazon, java, design pattern:
分角色，g
最后，再电梯算法，分单双号

先建模

电梯
当前几个人，当前向上还是向下
变的状态和固有属性
class, 4个实例

     内部按和外部按，是个区别
     如果在内部按上，先上再下

内部和外部按有优先级，外部对master是平等的

楼层
当前有几个客人

proxy
乘客按了后，决策发到哪个电梯

中控master
处理一系列事件：电梯状态汇报，内部请求，外部请求，输出是控制命令的状态，电梯只执行
内部也发到master，电梯简化
闲的时候停在最高或最低，或平均停，优化初始状态
根据电梯当前状态，计算完成当前请求的代价，选代价最小的

follow up:
电梯维修或扩容
解耦


设计停车场
分类，定义类，这个类的边界是什么

[Google] Suppose you are given a dictionary of words based on an alphabet with a fixed number of characters. Please write a method/function which will find the longest word in the dictionary such that it can be built from successively adding a single character to an existing word in the dictionary (in any location). For instance, “a” -> “at” -> “cat” -> “chat” -> “chart”. 
①拓扑排序
②按长度排序，搜索
③按长度降序，按层减字符，关键要减，如果子母集很大，就有问题


22. [Facebook] 
Given an array A of positive integers. Convert it to a sorted array with 
minimum cost. The only valid operation are:
1) Decrement with cost = 1
2) Delete an element completely from the array with cost = value of element
http://www.mitbbs.com/article_t/JobHunting/32061183.html

solution:
http://collabedit.com/kv27d

23. 烧绳子

24. [Amazon] 求树的最大宽度
层次遍历

25. [Facebook] 一个很大的文件，怎么去掉duplicate
每行是数字还是string
分割，hash， 桶内合并

27. [Google] Given P machines, each containing an array of N elements, find the medium of the array resulted by concatenating all the arrays on the machines. You cannot move data across machines. 
二分猜答案

28. [Amazon] 给一个二叉树，如何转化成mirror image
递归

29. 找二叉树两个最大的相同子树
后序遍历
存sign(root)
val, left, right

30. [Bloomberg] Find minimum number of characters that need to be inserted into a string (anywhere in the string) to make it a palindrome. 
(1) 翻转，求lcs
(2) dp

31. [Google] iterator has only hasNext() and Next() method, write a wrapper for iterator, to support .
http://collabedit.com/kv27d

32 Given a sequence of data (it may have duplicates), a fixed-sized moving window, move the window at each iteration from the start of the data sequence, such that

(1) the oldest data element is removed from the window and a new data element is pushed into the window
(2) find the median of the data inside the window at each moving. 
最大堆，最小堆

33. [Amazon, Microsoft] 将数组里的负数排在数组的前面，正数排在数组的后面，，单不改变原先负数和正数的排列顺序
input: -5, 2, -3, 4, -8, -9, 1, 3, -10
outpu: -5, -3, -8, -9, -10, 2, 4, 1, 3
归并

41. [Google] Given a dictionary and a string, write a program to output the valid words while minimizing the numbers of skipped characters. The substring that consists of a valid word in the dictionary may swap the characters. For example, Given a dictionary d = window, cat and a string “iwndowdcta”, the output is “window cat”. In this case, there is only one number of skipped character which is ’d’
dp dp[i] = min(dp[j] + sun(s[j:i] in dict ?0 : length)

42.[Microsoft] How to find if a number is present equal to or more than n/2 times in an array of size n? 

     先拿第一个数，判断是否出现n/2次，否则，扔掉，在找n/2大的数

43. given an array of n unsorted integers and each number is at most k positions away from its final sorted position, give an ecient sorting algorithm.
k堆

44. 安排演出
线段不重叠 

45. window substring
双指针

46. 处理一个字符串，删除里面所有的A，double所有的B
数个数

47. how to design a queue, in addition to insert and delete, also has a function min() which returns the minumum element? Can you do all functions in O(1) time? 
单调队列，递增

48. [Amazon] Write the code to count number of 1’s in binary expression of a given integer. 
while n > 0:
 n = n & (n-1)

49. [Amazon] Design file system. How about adding symbolic link 
文件系统:
数据文件
管理data

怎么存data
有大有小，挪动
分block，链起来组成大文件: 解决碎片和大文件问题

50. [Bloomberg] 8个球有一个比其他的重，用天平最少称几次能找出来
分4组

51. [Bloomberg] 1-100共100个数missing1个，如何找出来，missing 2个?
1. x + y, x^2 + y^2
2. bit数组

52. [Amazon] 怎么实现boolen isBST(Node *root) ?

53. [Amazon] Stream of characters, at any point you should be able to answer what is the most recent character that happened only once

54. [Google] Three coke machines. Each one has two values min & max, which means if 
you get coke from this machine it will load you a random volume in the range
[min, max]. Given a cup size n and minimum soda volume m, show if it's 
possible to make it from these machines.

比如三台machine(50, 100), (100, 200), (500, 1000). n=110, m=40, yes. n=90, m
=40, no. n=100, m=60, no.




58. [Google] 一个数组a1, a2, a3, …an, b1, b2, b3, …, bn，怎么inplace转化成a1, b2, a2, b2, …, an, bn
归并
(1) a1, a2, a3, …, ak,b1, b2, b3, …, bk, ak+1, ak+2, …bn
(2) 完美洗牌

59. N组正数，每组都由小到达排列，如何快速找到N组都有的最大整数
(1) 按最大的往左边扫
(2) 堆，存最大值

62. [Amazon] Given a list of points in 2D and a single reference point, find k nearest neighbors. 
(1) topk
(2) 堆
(3) sort
工程: 网格索引

64. 4 * 4的矩阵，左上走到右下，可以走上下左右四个方向，不能走走过的格子，有多少unique的走法?
搜索

65. [Microsoft] 有2*N个文件，文件的大小保存在size[2*N]中。然后想要分成N份(每一份可以有1个或多个文件),要使这N份中的文件size之和的最大值最小，如何实现?
(1) 二分猜答案

66. [Google] 找到字符串A在字符串B中出现的次数，可以重复使用字母，比如A: aba B: ababa，那么返回2.
(1) robin
(2) kmp
(3) bm

67. [Google] 
模拟

68. [Amazon] 
bfs

69. [Google]
dict

70. 
(1) 枚举
(2) n^2，对角线

71. 

72. 
杨式矩阵

73. [Microsoft] Describe a data structure for which 
getValue(int index)
setValue(int index, int value)
setAllValues(int value)
are all O(1)

array + timestamp


74. 
http://www.careercup.com/question?id=14485932

75. 
trie
strstr

76. 
中序遍历

77.

78.
匹配

79.
trie树
工程:
按什么排序，点击，个性化等



80.

81.
前缀和

82.
Given an array, find the longest subarray which the sum of the subarray less or equal then the given MaxSum. 
先求array sum=total，两个指针指向头尾。如果total<=MaxSum, return，否则将total减去较大的数，start++ or end--

83. [Facebook, Amazon]
写一个二叉树中序遍历的iterator
迭代遍历

84.
(1) 先找第一个数，删掉，再找第二个数
(2) 反过来的题，线段树
(3) 线段树
(4) 先找最小的

85.
 并查集

86.
hash

87.
(1) counting sort，按起始点排序
然后贪心，维护一个区间

88.
略

89. [Google] 一个大型cluster包括

90. [Google]
如何让server避免block
sensort的优先级，维护一个sensor队列，按失败次数排优先级，时间越长优先级越高，失败次数越多优先级越低

91. [Google] 设计题是一堆机器生成unique ID，这些机器之间不能互相通信，也没有master
uuid生成: 时间戳 + 机器标识(mac地址) + 进程id + 随机数 + counter

92. [Microsoft]

93. 
一次排2m

94.

95.
插入后往后移动

96.

97.

98.
变步长

99.

100.
HyperLogLog
http://antirez.com/news/75

101.
搜

104.
bloomfilter

106.
 
107. Reverse postfix order
pass

108.
搜

109.
http://blog.csdn.net/wcyoot/article/details/6435904

110.

111.
trie

112.
循环遍历

113.

114. 从n个无重复正整数

116.
2个数: 分成两组

117.
set，有就删掉，没有就删掉

118.
模k，划分等价类

