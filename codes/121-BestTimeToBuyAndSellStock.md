### 题目描述

Say you have an array for which the ith element is the price of a given stock on day i. 
If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit. 

>Example 1: 

- Input: [7, 1, 5, 3, 6, 4] 

- Output: 5

- max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)

>Example 2: 

- Input: [7, 6, 4, 3, 1] 

- Output: 0

- In this case, no transaction is done, i.e. max profit = 0. 

给定一个数组，数组中下标为i的元素表示第i天的股票的价钱。在只完成一笔交易的前提下，输出获得的最大利润。

### 解题思路

用minPrice变量记录从前向后遍历的时候最便宜的股票，用maxPro记录当前股票价钱与最便宜的股票的价钱之差

### 代码
```
int maxProfit(vector<int>& prices) {
        int maxPro=0,minPrice=INT_MAX;
        for(int i=0;i<prices.size();i++){
            minPrice=min(minPrice,prices[i]);
            maxPro=max(maxPro,prices[i]-minPrice);       
        }
        return maxPro;
}
```
