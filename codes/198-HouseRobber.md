You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

**Example 1**

  Input: [1,2,3,1] 
  
  Output: 4 
  
  Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3). 
               Total amount you can rob = 1 + 3 = 4.


**Example 2**

  Input: [2,7,9,3,1] 
  
  Output: 12 
  
  Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1). 
               Total amount you can rob = 2 + 9 + 1 = 12.


### 思路

类似leecode第746题，采取动态规划的方法，将nums数组每次更新为自己加上max（自己-2，自己-3）

从而保证nums数组代表的值为目前所能达到的最大值，然后返回nums数组末尾两个元素的最大值即可。

代码：

```C
int rob(vector<int>& nums) { 
        if(nums.size()==0)
            return 0;
        if(nums.size()>=3)
            nums[2]=nums[0]+nums[2];
        for(int i=3;i<nums.size();i++) { 
            nums[i]=nums[i]+max(nums[i-2],nums[i-3]); 
        }
        return nums[nums.size()-1]>nums[nums.size()-2]?nums[nums.size()-1]:nums[nums.size()-2];
    }
```
