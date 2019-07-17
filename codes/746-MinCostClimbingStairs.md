### 问题描述

On a staircase, the i-th step has some non-negative cost cost[i] assigned (0 indexed).  

Once you pay the cost, you can either climb one or two steps. You need to find minimum cost to reach the top of the floor, and you can either start from the step with index 0, or the step with index 1. 

**Example 1**

  Input: cost = [10, 15, 20]
  
  Output: 15 
  
  Explanation: Cheapest is start on cost[1], pay that cost and go to the top.


**Example 2**


  Input: cost = [1, 100, 1, 1, 1, 100, 1, 1, 100, 1] 
  
  Output: 6 
  
  Explanation: Cheapest is start on cost[0], and only step on 1s, skipping cost[3].


Note:


 - cost will have a length in the range [2, 1000]. 
 - Every cost[i] will be an integer in the range [0, 999].


从第0或者第1开始跳，每次跳1步或者2步，到达最后1个或者倒数第2个，求经过的数组元素之和的最小值。

### 思路

改变cost数组，之前cost数组的含义是在这里跳一步所要消耗的权值，修改之后的cost数组的含义是：在刚刚从这里跳出去了的情况下所使用的最小权值。例如cost[2]表示从第3个元素跳出去一步（可能跳在第4或者第5），此时消耗的权值的最小值。 

第1和第2不考虑，从第3个元素开始，cost数组下标为这个元素的值应该等于之前cost数组的权重，加上前两个元素中所需要的权值更小的那个。

```
int minCostClimbingStairs(vector<int>& cost) {
    for(int i=2;i<cost.size();i++) { 
        cost[i]=cost[i]+min(cost[i-1],cost[i-2]); 
    }
    return min(cost[cost.size()-1],cost[cost.size()-2]);
}
```
