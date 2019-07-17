### 问题描述

Given two arrays, write a function to compute their intersection.  

Example: 

Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2].  

>Note:Each element in the result must be unique.The result can be in any order.

### 代码

```
vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> s(nums1.begin(), nums1.end());
        vector<int> out;
        for (int x : nums2)
            if (s.erase(x))
                out.push_back(x);
        return out;    
    }
```
