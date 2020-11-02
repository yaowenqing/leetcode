### 问题描述

Given two arrays, write a function to compute their intersection.  

Example: 

Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2].  

>Note:Each element in the result must be unique.The result can be in any order.

### 代码

```C++
vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> s(nums1.begin(), nums1.end());
        vector<int> out;
        for (int x : nums2)
            if (s.erase(x))
                out.push_back(x);
        return out;    
    }
```

### java代码


利用Set不可重复、无序性的特点

```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> s1=new HashSet<Integer>();
        Set<Integer> s2=new HashSet<Integer>();
        for(int i=0;i<nums1.length;i++){
            s1.add(nums1[i]);
        }
        for(int i=0;i<nums2.length;i++){
            if(s1.contains(nums2[i]))
                s2.add(nums2[i]);
        }
        int[] res=new int[s2.size()];
        int count=0;
        for(int i:s2){
            res[count++]=i;
        }
        return res;
    }
}
```

