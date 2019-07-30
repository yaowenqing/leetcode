Given a non-empty array of non-negative integers nums, the degree of this array is defined as the maximum frequency of any one of its elements. 

Your task is to find the smallest possible length of a (contiguous) subarray of nums, that has the same degree as nums. 

一个由非负整数组成的非空数组，把数组的度定义为出现频率最高的数组元素。 

找出这个数组的最小子数组（这个子数组在原数组中必须是连续的），这个子数组的度和原数组一样。 

返回这个子数组的长度。 

**Example 1**

  Input: [1, 2, 2, 3, 1] 
  
  Output: 2 
  
  Explanation:The input array has a degree of 2 because both elements 1 and 2 appear twice. 
  
  the subarrays that have the same degree: 
  
  [1, 2, 2, 3, 1], [1, 2, 2, 3], [2, 2, 3, 1], [1, 2, 2], [2, 2, 3], [2, 2] 
  
  The shortest length is 2. So return 2.

**Example 2**

Input: [1,2,2,3,1,4,2] 

Output: 6

### 解题思路

首先找出数组的度。 

创建一个map，把出现过的数字作为map的第一维度，出现的数字在nums数组中所出现的地方作为第二维度（第二维度是一个vector）。找出第二维度中个数最多的第一维度数字，该数字出现的次数即为数组的度。 

遍历map，在所有map的第二维度个数等于数组的度的地方，算出出现的最后一个地方和出现的第一个地方之差+1，即为符合要求的子数组的长度。并与minLen进行min运算，如此反复，最终得到最小子数组的长度。


```
int findShortestSubArray(vector<int>& nums) {
        int degree=0;   //nums数组的度
        unordered_map<int,vector<int>>mp;
        for(int i=0;i<nums.size();i++) 
            mp[nums[i]].push_back(i);
        for(auto it=mp.begin();it!=mp.end();it++)
            degree=max(degree,int(it->second.size()));

        int minLen=nums.size(); //符合要求的最小子数组的长度
        for(auto it=mp.begin();it!=mp.end();it++){
            if(it->second.size()==degree)
                minLen=min(minLen,it->second.back()-it->second[0]+1);
        }     
        return minLen;
    }
```
