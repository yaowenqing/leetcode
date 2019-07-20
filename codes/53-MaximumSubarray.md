### 题目描述

Find the contiguous subarray within an array (containing at least one number) which has the largest sum.  

For example, given the array [-2,1,-3,4,-1,2,1,-5,4], 

the contiguous subarray [4,-1,2,1] has the largest sum = 6.

### 代码

一个非常巧的解法：

```
int maxSubArray(vector<int>& nums) {
        int res=nums[0],sum=0;
        for(int i=0;i<nums.size();i++){
            sum+=nums[i];
            res=max(res,sum);
            sum=max(sum,0);
        }
        return res;
    }
```  
  

也可以用动态规划来做：

```
int maxSubArray(vector<int>& nums) {
        if(nums.size()==1)
            return nums[0];

        vector<int>dp(nums.size());
        dp[0]=nums[0];
        int res=nums[0];
        for(int i=1;i<nums.size();i++){
            dp[i]=nums[i]+(dp[i-1]>0?dp[i-1]:0);
            res=max(dp[i],res);
        }
        return res;
    }
```
