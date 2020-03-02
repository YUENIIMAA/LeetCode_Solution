# LeetCode Solution
- 题目后第一个框框记录耗费**时间**在提交时击败选手的百分比
- 题目后第二个框框记录耗费**空间**在提交时击败选手的百分比

#1 Two Sum `92.82%` `39.78%`

#2 Add Two Numbers `88.95%` `5.14%`

#3 Longest Substring Without Repeating Characters `82.53%` `59.20%`

#4 Median of Two Sorted Arrays `99.86%` `84.54%`

#5 Longest Palindromic Substring `91.17%` `62.76%`

#6 ZigZag Conversion `94.01%` `100%`

简单分发后拼起来效率也挺高，但应注意到每组有（2 x 行数 - 2）个字符，分组后组内的前行数个字符就是组成`|`的字符，剩下的对应`/`中的字符，且同行同组的两个字符位置存在固定计算方式。于是可以用行数外循环，每行`|`上元素内循环，无需分发直接组合出结果。

\#7 Reverse Integer `100%` `100%`

注意如何在不实际溢出的情况下预判将要溢出的情况。

#8 String to Integer (atoi) `100%` `100%`

规则要理解清楚，最开始的空格都可以忽略，第一个不是空格的只能是符号或数字，否则不合法，一旦接触到数字或符号后再遇到其他字符则应停止转换。

\#9 Palindrome Number `90.24%` `100%`

整个反转会有溢出风险，并且重点不是找到中心位置。规避前者只要不断地拿走个位数使原数字变小，取得和后者相同的效果只要用取下的数字构建出一个镜像数字与原数字剩下的一半比较即可。

#11 Container With Most Water `96.33%` `100.00%`

#12 Integer to Roman `76.39%` `100.00%`

#13 Roman to Integer `57.95%` `41.18%`

#14 Longest Common Prefix `100.00%` `100.00%`