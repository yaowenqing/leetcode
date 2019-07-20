### 题目描述

Given a binary array, find the maximum number of consecutive 1s in this array. 

**Example 1**

  Input: [1,1,0,1,1,1] 
  
  Output: 3 
  
  Explanation: The first two digits or the last three digits are consecutive 1s. 
      The maximum number of consecutive 1s is 3.

Note: 


  - The input array will only contain 0 and 1. 
  - The length of input array is a positive integer and will not exceed 10,000

### 代码

```
int findMaxConsecutiveOnes(vector<int>& nums) {
        int sign=0,max=0;
        for(int i=0;i<nums.size();i++){
            if(nums[i]==1)
                max=++sign>max?sign:max;
            else
                sign=0;
        }
        return max;
    }
```
