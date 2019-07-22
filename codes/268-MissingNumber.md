### 问题描述

Given an array containing n distinct numbers taken from 0, 1, 2, …, n, find the one that is missing from the array.

**Example 1**

Input: [3,0,1]

Output: 2

**Example 2**

Input: [9,6,4,2,3,5,7,0,1]

Output: 8

- Note:Your algorithm should run in linear runtime complexity. Could you implement it using only constant extra space complexity?

思路：n个数字相加的和减去nums数组中所有数字相加的和即为结果。

### 代码

```
int missingNumber(vector<int>& nums) {
        int n=nums.size(),sum1=0,sum2=0;
        for(int i=1;i<n+1;i++){
            sum1+=i;
        }
        for(int i=0;i<n;i++){
            sum2+=nums[i];
        }
        return sum1-sum2;
    }
```
