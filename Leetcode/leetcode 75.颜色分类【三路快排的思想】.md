# 原创：leetcode 75.颜色分类【三路快排的思想】

最开始的想法是快排的双指针思想，奈何里面有三种元素，双指针搞不定：

> 
看了一下参考答案，发现和我的想法很类似：
本问题被称为 [荷兰国旗问题](https://en.wikipedia.org/wiki/Dutch_national_flag_problem) ，最初由 [Edsger W. Dijkstra](https://baike.baidu.com/item/%E8%89%BE%E5%85%B9%E6%A0%BC%C2%B7%E8%BF%AA%E7%A7%91%E6%96%AF%E5%BD%BB/5029407?fromtitle=Dijkstra&amp;fromid=1880870&amp;fr=aladdin)提出。 其主要思想是给每个数字设定一种颜色，并按照荷兰国旗颜色的顺序进行调整。

用三个指针（p0, p2 和curr）来分别追踪0的最右边界，2的最左边界和当前考虑的元素。
沿着数组移动 `curr` 指针，若`nums[curr] = 0`，则将其与 `nums[p0]`互换；若 `nums[curr] = 2` ，则与 `nums[p2]`互换。
**1则跳过**


开始动手实现：

执行用时 : 4 ms, 在Sort Colors的C++提交中击败了97.62% 的用户

内存消耗 : 8.7 MB, 在Sort Colors的C++提交中击败了8.05% 的用户

 
