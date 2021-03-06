### 问题描述

Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).

>Note: You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

**Example 1:**

Input: [7,1,5,3,6,4]

Output: 7

Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.

  Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.

**Example 2:**

Input: [1,2,3,4,5]

Output: 4

Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.

  Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are engaging multiple transactions at the same time. You must sell before buying again.

**Example 3:**

Input: [7,6,4,3,1]

Output: 0

Explanation: In this case, no transaction is done, i.e. max profit = 0.

**分析**

由于不能同时进行多笔交易，该题考查数组中所有相邻且递增元素的数值之差的总和。只要第i+1天的值大于第i天的值，则可买入，求得利润（差值），遍历整个数组，得到所用差值之和即为总的利润。

**代码**

```
int maxProfit(vector<int>& prices) {
        if (prices.size() <= 1)  
            return 0;  

        int profit=0;
        for(int i=0;i<prices.size()-1;i++){
            if(prices[i+1]>prices[i])
                profit+=prices[i+1]-prices[i];
        }
        return profit;
    }
```


