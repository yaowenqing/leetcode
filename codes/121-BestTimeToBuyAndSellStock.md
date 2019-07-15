### 题目描述

Say you have an array for which the ith element is the price of a given stock on day i. 
If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit. 

- Example 1: 
Input: [7, 1, 5, 3, 6, 4] 
Output: 5
max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)

> Example 2: 
Input: [7, 6, 4, 3, 1] 

Output: 0

In this case, no transaction is done, i.e. max profit = 0. 
给定一个数组，数组中下标为i的元素表示第i天的股票的价钱。在只完成一笔交易的前提下，输出获得的最大利润。在example1里面利润为6-1，不是7-1的原因是价值为7的那一天出现的时间在价值为1的那一天出现的时间之前。

解题思路：看代码即可看懂。



int maxProfit(vector<int>& prices) {
        int maxPro=0,minPrice=INT_MAX;
        for(int i=0;i<prices.size();i++){
            minPrice=min(minPrice,prices[i]);
            maxPro=max(maxPro,prices[i]-minPrice);       
        }
        return maxPro;
}
