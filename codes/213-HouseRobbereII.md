You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. 
All houses at this place are arranged in a circle. 
That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

动态规划，类似第198题，分两种情况，第一种从第一家抢到第n-1家，第二种从第二家抢到第n家，取两种情况能抢到的最多的钱，这样可以保证即使围成了圆圈也不会抢到相邻两家。

```
int rob(vector<int>& nums) {
        int n=nums.size();
        if(n<1)
            return 0;
        if(n==1)
            return nums[0];
        if(n==2)
            return max(nums[0],nums[1]);
        int dp[n];
        int dp2[n];   
        dp[0]=nums[0];
        dp[1]=max(nums[0],nums[1]);
        for(int i=2;i<n-1;i++){
            dp[i]=max(dp[i-2]+nums[i],dp[i-1]);
        }
        
        dp2[0]=nums[1];
        dp2[1]=max(nums[1],nums[2]);
        for(int i=3;i<n;i++){
            dp2[i-1]=max(dp2[i-3]+nums[i],dp2[i-2]);
        }
        return max(dp[n-2],dp2[n-2]);
    }
```
