# LeetCode Solution
- 题目后第一个框框记录耗费**时间**在提交时击败网友的百分比
- 题目后第二个框框记录耗费**空间**在提交时击败网友的百分比

**\#1 Two Sum** `92.82%` `39.78%`

用Hash Table加速检索，一边插入一边检索可以实现插完查完出结果。

**\#2 Add Two Numbers** `88.95%` `5.14%`

**\#3 Longest Substring Without Repeating Characters** `82.53%` `59.20%`

滑窗的方式，头和尾一起前进。

**\#4 Median of Two Sorted Arrays** `99.86%` `84.54%`

注意到给出的两个数组已排序，直接快速合并取中位数就好。

**\#5 Longest Palindromic Substring** `91.17%` `62.76%`

先寻找中心块，可为空，然后向左右延申寻找最长的对称字符串，计算当前长度和历史最长进行比较，更大就覆盖。

**\#6 ZigZag Conversion** `94.01%` `100.00%`

简单分发后拼起来效率也挺高，但应注意到每组有（2 x 行数 - 2）个字符，分组后组内的前行数个字符就是组成`|`的字符，剩下的对应`/`中的字符，且同行同组的两个字符位置存在固定计算方式。于是可以用行数外循环，每行`|`上元素内循环，无需分发直接组合出结果。

**\#7 Reverse Integer** `100.00%` `100.00%`

注意如何在不实际溢出的情况下预判将要溢出的情况。

**\#8 String to Integer (atoi)** `100.00%` `100.00%`

规则要理解清楚，最开始的空格都可以忽略，第一个不是空格的只能是符号或数字，否则不合法，一旦接触到数字或符号后再遇到其他字符则应停止转换。

**\#9 Palindrome Number** `90.24%` `100.00%`

整个反转会有溢出风险，并且重点不是找到中心位置。规避前者只要不断地拿走个位数使原数字变小，取得和后者相同的效果只要用取下的数字构建出一个镜像数字与原数字剩下的一半比较即可。

**\#10 Regular Expression Matching** `100.00%` `100.00%`

甚难，首先想到动态规划，然后想到不能反复递归调用，不然会重复计算，必须自底向上才能暂存结果。于是开辟(lenS + 1) x (lenP + 1)大小的数组（其实可以只开3行来大幅减少空间复杂度，因为新一行结果最多只需要用到前两行的结果），设置第0行和第0列均为false（因为空字符串匹配非空正则一般都是不匹配，特殊情况后面处理，而正则实际不为空的情况匹配字符串空位一定是false），然后初始化isMatch\[0\]\[0\]为true。处理a\*b \* ce\*这种特殊情况，即非空正则匹配空字符串，一旦检测到\*，就把当前位置和前一个位置均设置成向前两格的值。初始化完毕后开始逐行叠加，不出现\*时，只要当前字符和正则符匹配，则匹配情况同各减去一个字符的情况，若出现了\*，分两种情况，一种是正则的前一个字符与当前字符匹配，则可能是它重复出现的情况或者重复0或1次的情况，不匹配的情况考虑是否出现0次取正则向前两个字符的结果。

**\#11 Container With Most Water** `96.33%` `100.00%`

从左右向内夹逼，每次更短地前进，相同高度情况下下一格更高的前进。

**\#12 Integer to Roman** `76.39%` `100.00%`

一级一级往下减减到0，一边减一边生成罗马数字。

**\#13 Roman to Integer** `57.95%` `41.18%`

Hash Table加速检索，先处理特殊情况，单字符直接返回。其余情况下若后一个数字比自己大则总数减去自己，否则加上自己。

**\#14 Longest Common Prefix** `100.00%` `100.00%`

纵向扫描。

**\#15 3Sum** `99.66%` `100.00%`

先排序，C++有内置的没必要造轮子。排序后从头向后遍历，以自己为目标数，对自己以后的内容做已排序的2Sum：前后向内夹逼，和大于则大数后退，和小于则小数前进，和等于向内去重后各靠近一步。大的遍历到0就可以停止，因为大于0的数之后也全大于0，和不可能是0。另外大的遍历中和前一位数字一样的可以跳过，这样导出的结果一定是没有重复的。

**\#16 3Sum Closest** `99.13%` `100.00%`

基于3Sum小改一下即可，去掉超过目标就停止的限制，修改大小于的情况为计算差值与最小差值比较并更新最小差值和最接近数字，遇到相等的情况直接返回目标。

**\#18 4Sum** `86.75%` `100.00%`

把3Sum和3Sum Closest整合在一起，注意原3Sum有一个中断机制，在4Sum里这个中断机制要考虑当前值小于0并且目标值也小于0的情况，使用原判断方式会在目标数小于当前值小于0时直接中断，但当前值再加一个负数时可能达到目标值的。

**\#20 Valid Parentheses** `100%` `100.00%`

用堆，左边压入右边弹出，弹出的不是自己另一半就错，最后有剩的也错，注意堆一开始可以放一个无关紧要的，防止一上来就是右半边但是栈顶没东西导致出错。

**\#21 Merge Two Sorted Lists** `48.80%` `40.16%`

**\#23 Merge k Sorted Lists** `90.57%` `5.95%`

可选模仿合并两个已排序链表的方式，但用优先队列实现起来会更加方便一些。

**\#28 Implement strStr()** `90.55%` `100.00%`

**\#29 Divide Two Integers** `100.00%` `100.00%`

被除数a可以表示为除数b的如下形式：a= b* 2^m + b*2^n...，后面的每一项都可以用对b的位操作快速实现，因此可以快速减小被除数a，而2^m本身又可以表示成对1的位操作，最终可以用较少的加法和减法快速组合出答案，注意在求m的时候循环结束后m要减一，因为循环体跳出时减数已经大于被减数了。

**\#35 Search Insert Position** `98.18%` `100.00%`

二分查找，把小于最小的和大于最大的单独先处理掉，内部二分查找时下限要增加，上限不要动。

**\#36 Valid Sudoku** `90.83%` `100.00%`

最开始用了set来插入已出现的数字，但这样每次需要检索才能确定是否重复出现。因此改用vector，用数字作为下表，真假记录是否出现，就可以在固定时间查找出结果，速度更快。另外了解到了除了下标操作符[]还有成员函数at()这样的用法，后者会检查下标是否越界，比如对长度为8的字符串s，s[8]会返回'\0'不报错，而s.at(8)则会报越界错误。

**\#46 Permutations** `98.65%` `100.00%`

算法书上教过的算法，重点是如果只用它给出的函数反复递归，需要对nums进行反复的元素删除和插入操作，耗时耗空间，因此一定要自己额外写一个适合递归的私有函数让给出的函数来调用，注意参数的设置，注意容器中push_back和emplace_back的区别。

**\#47 Permutations II** `95.19%` `100.00%`

首先补充上面的内容，上面的做法还避免了重新组合出一个完整排序再插入的过程，是直接对原nums做若干swap之后放进返回集合中并恢复nums的高级做法。虽然直觉上想要先对输入数组进行排序，但实际上没有必要，去除重复的关键是每个每个数字在每一个位置只能被处理一次，因此函数需要有另一个vector来记住自己已经处理过的数字。

**\#50 Pow(x, n)** `100.00%` `100.00%`

每次减半n然后自己乘自己来快速缩减时间复杂度，n为单数的时候额外再乘一次x就行了。另外最重要的是注意到应使用位操作来快速计算n除以2的结果和判断n是否为奇数。