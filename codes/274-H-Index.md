### 问题描述

Given an array of citations (each citation is a non-negative integer) of a researcher, write a function to compute the researcher’s h-index.

According to the definition of h-index on Wikipedia: “A scientist has index h if h of his/her N papers have at least h citations each, and the other N−h papers have no more than h citations each.”

Example: Input: citations = [3,0,6,1,5]

Output: 3

Explanation: [3,0,6,1,5]means the researcher has 5 papers in total and each of them had received 3, 0, 6, 1, 5 citations respectively. Since the researcher has 3 papers with at least 3 citations each and the remaining two with no more than 3 citations each, her h-index is 3.


Note: If there are several possible values for h, the maximum one is taken as the h-index.

给定一个数组，记载了某研究人员的文章引用次数（都是非负整数），编写函数计算该研究人员的h指数。

维基百科上对h指数的定义：“一名科学家的h指数是指在其发表的N篇论文中，有h篇论文分别被引用了至少h次，其余N-h篇的引用次数均小于h次”。

例如，给定一个数组citations = [3, 0, 6, 1, 5]，这意味着该研究人员总共有5篇论文，每篇分别获得了3, 0, 6, 1, 5次引用。由于研究人员有3篇论文分别至少获得了3次引用，其余两篇的引用次数均不超过3次，因而其h指数是3。

注意：如果存在多个可能的h值，取最大值作为h指数。

### 解题思路

把数组中的元素从小到大排列。然后依次遍历，如果排序好的数组中第i+1个元素的值（即citations[i]）大于等于n-i，证明至少有n-i个元素（即后面还没被遍历的元素个数）的值大于等于n-i，n-i即为h-index值。代码如下：

### 代码
```
int hIndex(vector<int>& citations) {
        sort(citations.begin(), citations.end());        
        int n=citations.size();
        for(int i=0;i<n;i++){
            if(citations[i]>=n-i)
                return n-i;
        }
        return 0;
    }
```
