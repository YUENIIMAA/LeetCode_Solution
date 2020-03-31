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

简单分发后拼起来效率也挺高，但应注意到每组有（2 x 行数 \- 2）个字符，分组后组内的前行数个字符就是组成`|`的字符，剩下的对应`/`中的字符，且同行同组的两个字符位置存在固定计算方式。于是可以用行数外循环，每行`|`上元素内循环，无需分发直接组合出结果。

**\#7 Reverse Integer** `100.00%` `100.00%`

注意如何在不实际溢出的情况下预判将要溢出的情况。

**\#8 String to Integer (atoi)** `100.00%` `100.00%`

规则要理解清楚，最开始的空格都可以忽略，第一个不是空格的只能是符号或数字，否则不合法，一旦接触到数字或符号后再遇到其他字符则应停止转换。

**\#9 Palindrome Number** `90.24%` `100.00%`

整个反转会有溢出风险，并且重点不是找到中心位置。规避前者只要不断地拿走个位数使原数字变小，取得和后者相同的效果只要用取下的数字构建出一个镜像数字与原数字剩下的一半比较即可。

**\#10 Regular Expression Matching** `100.00%` `100.00%`

甚难，首先想到动态规划，然后想到不能反复递归调用，不然会重复计算，必须自底向上才能暂存结果。于是开辟\(lenS \+ 1\) x \(lenP \+ 1\)大小的数组（其实可以只开3行来大幅减少空间复杂度，因为新一行结果最多只需要用到前两行的结果），设置第0行和第0列均为false（因为空字符串匹配非空正则一般都是不匹配，特殊情况后面处理，而正则实际不为空的情况匹配字符串空位一定是false），然后初始化isMatch\[0\]\[0\]为true。处理a\*b \* ce\*这种特殊情况，即非空正则匹配空字符串，一旦检测到\*，就把当前位置和前一个位置均设置成向前两格的值。初始化完毕后开始逐行叠加，不出现\*时，只要当前字符和正则符匹配，则匹配情况同各减去一个字符的情况，若出现了\*，分两种情况，一种是正则的前一个字符与当前字符匹配，则可能是它重复出现的情况或者重复0或1次的情况，不匹配的情况考虑是否出现0次取正则向前两个字符的结果。

**\#11 Container With Most Water** `96.33%` `100.00%`

从左右向内夹逼，每次更短地前进，相同高度情况下下一格更高的前进。

**\#12 Integer to Roman** `76.39%` `100.00%`

一级一级往下减减到0，一边减一边生成罗马数字。

**\#13 Roman to Integer** `57.95%` `41.18%`

Hash Table加速检索，先处理特殊情况，单字符直接返回。其余情况下若后一个数字比自己大则总数减去自己，否则加上自己。

**\#14 Longest Common Prefix** `100.00%` `100.00%`

纵向扫描。

**\#15 3Sum** `99.66%` `100.00%`

先排序，C\+\+有内置的没必要造轮子。排序后从头向后遍历，以自己为目标数，对自己以后的内容做已排序的2Sum：前后向内夹逼，和大于则大数后退，和小于则小数前进，和等于向内去重后各靠近一步。大的遍历到0就可以停止，因为大于0的数之后也全大于0，和不可能是0。另外大的遍历中和前一位数字一样的可以跳过，这样导出的结果一定是没有重复的。

**\#16 3Sum Closest** `99.13%` `100.00%`

基于3Sum小改一下即可，去掉超过目标就停止的限制，修改大小于的情况为计算差值与最小差值比较并更新最小差值和最接近数字，遇到相等的情况直接返回目标。

**\#17 Letter Combinations of a Phone Number** `100.00%` `100.00%`

虽然是暴力求解，但是暴力得高效省空间，很好地实践了\#22里学到的方法。

**\#18 4Sum** `86.75%` `100.00%`

把3Sum和3Sum Closest整合在一起，注意原3Sum有一个中断机制，在4Sum里这个中断机制要考虑当前值小于0并且目标值也小于0的情况，使用原判断方式会在目标数小于当前值小于0时直接中断，但当前值再加一个负数时可能达到目标值的。

**#19 Remove Nth Node From End of List** `94.41%` `100.00%`

直觉做法是一次性遍历把所有指针都丢进vector然后直接用下标操作，实际实现结果和后面不使用vector几乎一致。稍微省点空间但是并没有更快的做法是用两个指针，第一个指针比第二个指针先n步出发，这样第一个指针到底时第二个指针刚好在从后往前第n+1位，对其进行操作即可，思路是个好思路。

**\#20 Valid Parentheses** `100.00%` `100.00%`

用堆，左边压入右边弹出，弹出的不是自己另一半就错，最后有剩的也错，注意堆一开始可以放一个无关紧要的，防止一上来就是右半边但是栈顶没东西导致出错。

**\#21 Merge Two Sorted Lists** `48.80%` `40.16%`

**#22 Generate Parentheses** `87.79%` `86.78%`

一种递归的想法是当n为0时返回空，否则在自己内部和自己右边递归调用生成函数，然后重组。该解法在C\+\+实现下没能取得较好的运算效率。后来看到了两个跑得贼快的解法，二者都是根据开闭端数量快速生成结果的方法，详见Reference Better Solution，这两个算法效率高的核心原因都是避免了反复将元素加入vector再取出。或许以后所有生成排序集合的题都要考虑用string暂存结果，vector始终靠引用传递，在递归的最后才放入vector的方式。同时也学到了二叉树的实现，没必要在数据结构里放指向下一个的指针，放进堆里可以用位置来推断节点在二叉树中的位置。

**\#23 Merge k Sorted Lists** `90.57%` `5.95%`

可选模仿合并两个已排序链表的方式，但用优先队列实现起来会更加方便一些。

**\#26 Remove Duplicates from Sorted Array** `99.16%` `100.00%`

直觉会是从前往后比较，重复的就地删除，但从vector里反复删除元素是开销巨大的。可以用两个指针，一个标记某一个数字第一次出现的位置，另一个标记后一个数字第一次出现的位置，然后把后一个数字swap到前面去。这样整理完之后只需要在整理完之后执行一次erase就可以得到想要的结果。注意万恶的空输入情况需单独处理。

**\#27 Remove Element** `70.29%` `100.00%`

后来发现这个题好像只要重排就够了不需要手动删除元素。核心是把非val的数字往前换。

**\#28 Implement strStr\(\)** `90.55%` `100.00%`

**\#29 Divide Two Integers** `100.00%` `100.00%`

被除数a可以表示为除数b的如下形式：a = b \* 2^m + b \* 2^n\.\.\.，后面的每一项都可以用对b的位操作快速实现，因此可以快速减小被除数a，而2^m本身又可以表示成对1的位操作，最终可以用较少的加法和减法快速组合出答案，注意在求m的时候循环结束后m要减一，因为循环体跳出时减数已经大于被减数了。

**\#31 Next Permutation** `98.84%` `100.00%`

从后向前找第一个比前一位小的数字，然后反向寻找比它大的最小数字，交换后对它之后的数字升序排列。

**\#33 Search in Rotated Sorted Array** `80.37%` `100.00%`

本质上依旧是二分查找，但是额外多了一步判断往中间的哪个方向二分查找。如果最左位比中位小，则左半部分是升序的；如果最右位比中位大，则右半部分是升序的。

**\#34 Find First and Last Position of Element in Sorted Array** `85.93%` `100.00%`

二分查找法新的用法，可以查找下界和上界。

**\#35 Search Insert Position** `98.18%` `100.00%`

二分查找，把小于最小的和大于最大的单独先处理掉，内部二分查找时下限要增加，上限不要动。

**\#36 Valid Sudoku** `90.83%` `100.00%`

最开始用了set来插入已出现的数字，但这样每次需要检索才能确定是否重复出现。因此改用vector，用数字作为下表，真假记录是否出现，就可以在固定时间查找出结果，速度更快。另外了解到了除了下标操作符[]还有成员函数at()这样的用法，后者会检查下标是否越界，比如对长度为8的字符串s，s[8]会返回'\0'不报错，而s.at(8)则会报越界错误。

**\#38 Count and Say** `100.00%` `100.00%`

普通的数数加递归调用，这里可以实践之前学到的：对于字符串，如果使用下标操作符\[\]，越界一个字符（即访问string\[string\.size\(\)\]）是会得到\0而不报错的，因此不必担心对最后一个字符判断后一位是否与其相同时需要单独处理。

**\#39 Combination Sum** `97.64%` `38.89%`

翻译一下这个问题就是每个数字选还是不选，选的话选几次，才能组成那个目标。于是就可以拆分成子问题了：首先排序，方便提前终止，一旦不选这个数字，就相当于从候选数中移除（跳过）自己，同时目标数不变，交给子问题解决；而选这个数字，则从目标数中减去自己，然后把相同的候选人交给子问题，这样可以兼顾选择若干次的情况。跳出条件是目标数比当前候选人中的一位小（放弃该选法）和目标数在选择候选人后降为0（把此时的集合放入ret）。注意当抵达最后一个数字时，不应出现不选自己的情况，不然会下标越界，该种情况包含于所有之前满足的集合里。（但是不知道为什么我的空间占用会那么大...）

**\#40 Combination Sum II** `83.15%` `13.16%`

大体基于前一题框架，由于每个元素只能被选一次，因此pick的情况就直接从下一位开始了。另外为了去除重复，一旦决定跳过一个元素，这个元素之后全部与它重复的元素都要跳过。

**\#41 First Missing Positive** `100.00%` `100.00%`

大爱此题，要巧妙利用下标，把数字a放到下标a-1的位置去，超过数组界限的元素不管，这样只需要遍历两次，第一次整理元素，第二次找下标和数字不匹配的第一个元素位置就是答案。这个做法的另一个妙处是不需要用特殊数字来标记空的位置，因为不管它也是标记错误的一种方式，以及不要去在意数字是往前换还是往后换，理论上往前换不需要在相同位置再执行循环体，往后换要，但为了区分这两种情况需要很多额外的判断，反而增加了overhead，而统一在交换后原地再次执行循环体只会增加至多一次额外的判断，overhead反而小，很妙的题。

**\#46 Permutations** `98.65%` `100.00%`

算法书上教过的算法，重点是如果只用它给出的函数反复递归，需要对nums进行反复的元素删除和插入操作，耗时耗空间，因此一定要自己额外写一个适合递归的私有函数让给出的函数来调用，注意参数的设置，注意容器中push\_back和emplace\_back的区别。

**\#47 Permutations II** `95.19%` `100.00%`

首先补充上面的内容，上面的做法还避免了重新组合出一个完整排序再插入的过程，是直接对原nums做若干swap之后放进返回集合中并恢复nums的高级做法。虽然直觉上想要先对输入数组进行排序，但实际上没有必要，去除重复的关键是每个每个数字在每一个位置只能被处理一次，因此函数需要有另一个vector来记住自己已经处理过的数字。

**\#48 Rotate Image** `81.81%` `100.00%`

拆分成从外向内的n/2层正方形，循环体是上方的倒三角，每一次循环完成4次交换。

**\#49 Group Anagrams** `99.48%` `94.03%`

对每个string本身执行sort形成一个key，这样字符组成相同排序不同的字符串就会被转换为相同且唯一的字符串作为key，记录这个key对应在vector中的下标就可以实现快速对号入座。

**\#50 Pow\(x, n\)** `100.00%` `100.00%`

每次减半n然后自己乘自己来快速缩减时间复杂度，n为单数的时候额外再乘一次x就行了。另外最重要的是注意到应使用位操作来快速计算n除以2的结果和判断n是否为奇数。

**\#53 Maximum Subarray** `98.45%` `100.00%`

对每个元素记录一个新的状态（可以直接覆盖在nums里面），以当前元素为最末位的组合的最大值，默认是原先自己的值，如果接在前一个元素（注意此时前一个元素的状态已经是以它为末位的组合的最大值了）能让当前状态变大，则以新的值覆盖当前值，意味着接在前面可以让自己更大，否则保留默认值，意味着与前面组合会减少自己，应新开一个子组合，这个有点难描述看代码会直观一些。

**\#54 Spiral Matrix** `100.00%` `100.00%`

又掉坑里，没有明确表明输入不为空的都要做空输入的特殊处理！

**\#58 Length of Last Word** `67.45%` `100.00%`

**\#62 Unique Paths** `100.00%` `100.00%`

仔细想想初中教的这种题用到的原来是动态规划的思想。

**\#66 Plus One** `100.00%` `100.00%`

只要不产生进位就立刻要跳出循环，另外因为明确了只加1，所以不用计算每一位减10，直接置零，而且连续进位一定是若干个九连续，所以如果在第一位还产生进位，那一定全是九，把第一位改1最后面补一个0也可以。

**\#67 Add Binary** `78.99%` `100.00%`

**\#69 Sqrt\(x\)** `100.00%` `100.00%`

牛顿迭代法，是什么一搜就有，还有一个要注意的是初值的选取和循环的跳出条件，初值选被开方数的一半（用位操作）可以使得迭代过程中仅有最后一次出现猜测值的平方小于等于被开方数，于是循环条件精简为一次平方计算，使得算法效率从73%左右的位置直接提升到100%，哦还有就是注意中间变量不能用整形，有溢出风险。

**\#70 Climbing Stairs** `100.00%` `100.00%`

动态规划，初值1个台阶1种，2个台阶2种，第n的台阶的走法是第n\-1个台阶与第n\-2的台阶的走法之和。

**\#73 Set Matrix Zeroes** `88.50%` `100.00%`

主要考验如何减少空间复杂度，首先遍历第一行和第一列，用两个布尔值记录它们是否需要被置零，然后遍历剩余的部分，用第一行和第一列来暂存是否要清除改行该列，以较小的代价解决了用0标记和本身是0的冲突。

**\#75 Sort Colors** `63.93%` `100.00%`

没有注意到只有三种数值直接涂了快排上去，因此跑得不算快，实际上可以记录第一个非0的位置和最后一个非2的位置然后只对0和2进行归位，1会自动排好。

**\#78 Subsets** `97.23%` `100.00%`

每一个数两种状态，选或者不选。

**\#79 Word Search** `84.92%` `100.00%`

利用全局变量减少需要传递的参数和需要创建的变量。

**\#83 Remove Duplicates from Sorted List** `91.34%` `100.00%`

只用一个ptr的方法：不断地吞掉后面和自己重复的直到后一位与自己不同再移动到下一个位置。

**\#88 Merge Sorted Array** `84.71%` `100.00%`

发散一下思维，通常会选择头上开始选小的放到前面，但也可以从尾巴上开始选大的放到最后。

**\#91 Decode Ways** `60.89%` `100.00%`

动态规划，可能递推关系还是想复杂了各种优化跑不快。

**\#94 Binary Tree Inorder Traversal** `100.00%` `100.00%`

这题坑爹在居然真的会测空的树。

**\#98 Validate Binary Search Tree** `89.05%` `97.92%`

中序遍历，暂存前一位结果，一旦当前不大于前序则说明不是二叉搜索树。

**#100 Same Tree** `100.00%` `100.00%`

这也只能一个一个比下去了吧。