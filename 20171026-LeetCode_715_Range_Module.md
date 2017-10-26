## [LeetCode 715. Range Module](https://leetcode.com/problems/range-module/description/)

题目要求高效地实现区间的添加，删除和查询操作。

题目分析：本题是一道设计题，要求实现一个类(Range Module)的三个方法：addRange(int, int), queryRange(int, int) 和 removeRange(int, int)。
  该类的对象会穿插地调用这三个方法。听起来有点像并查集，但并查集“一般”不涉及删除操作（不是很确定，只能说“一般”），这道题其实用简单的map就可以实现。
  具体来说：map的key是区间的起点，value是区间的终点（其实用set也可以实现，set的元素是个pair<int, int>,自己实现比较函数即可）。
  由于map的key是有序的，所以在添加，删除或者查询区间的时候可以用log(n)的时间快速定位到用执行区间操作的位置。
  
  在每次进行区间操作（add, remove or query）之前，区间与区间之间都没有重叠部分，且区间与区间不相邻。
  
  addRange(int left, int right)：如果对象里没有一个区间，则直接插入要加的区间即可。
    否则，利用map<int, int>的lower_bound(int)函数可以查找到第一个左区间大于或者等于left位置（时间复杂度是log(n)），接下来分三种情况：
    1. 如果
