### 问题描述

Given an array of integers and an integer k, find out whether there are two distinct indices i and j in the array such that nums[i] = nums[j] and the absolute difference between i and j is at most k.（i和j的距离在k以内）

**Example 1**

Input: nums = [1,2,3,1], k = 3

Output: true

**Example 2**

Input: nums = [1,0,1,1], k = 1

Output: true

**Example 3**

Input: nums = [1,2,3,1,2,3], k = 2

Output: false

### 思路

用unordered_set，并且始终保持set中的元素在k个以内，一旦超过k，就删除前面的元素，这样保证了set中不会有下标距离之差大于k的元素。

代码如下：

```
    bool containsNearbyDuplicate(vector<int>& nums, int k) {
            unordered_set<int> s;
            if(k<=0)
                return false;
            if(k>=nums.size())
                k=nums.size()-1;
            
            for(int i=0;i<nums.size();i++){
                if(i>k)
                    s.erase(nums[i-k-1]);
                if(s.find(nums[i])!=s.end())
                    return true;
                s.insert(nums[i]);
            }
            return false;
        }
```
