### 问题描述

Given an array of integers, find if the array contains any duplicates. 

Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

**Example 1**

  Input: [1,2,3,1] 
  
  Output: true

**Example 2**

  Input: [1,2,3,4] 
  
  Output: false

**Example 3**

  Input: [1,1,1,3,3,4,3,2,4,2] 
  
  Output: true

### 思路

解决方案： 

一：双层循环，时间复杂度太高，放弃 

二：先排序后再单层遍历，时间复杂度nlogn，还是偏高 

三：使用unorder_set，代码如下

```
bool containsDuplicate(vector<int>& nums) {
        unordered_set<int>set;
        for(auto num:nums){
            if(set.find(num)!=set.end())
                return true;
            set.insert(num);
        }
        return false;
    }
```
