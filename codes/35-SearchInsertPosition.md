### 问题描述

Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order. 
You may assume no duplicates in the array. 

- Example 1:  

Input: [1,3,5,6], 5 

Output: 2

- Example 2:  

Input: [1,3,5,6], 2 

Output: 1

- Example 3:  

Input: [1,3,5,6], 7 

Output: 4

- Example 4:  

Input: [1,3,5,6], 0 

Output: 0

### 最容易想到的一般解法

int searchInsert(vector<int>& nums, int target) {
        for(int i=0;i<nums.size();i++){
            if(target<=nums[i])
                return i;
        }
        return nums.size();
    }1234567



### 二分查找

时间复杂度为logn

```
int searchInsert(vector<int>& nums, int target) {
        int low=0,high=nums.size()-1,mid;
        while(low<=high){
            mid=low+(high-low)/2;
            if(nums[mid]<target)
                low=mid+1;
            else 
                high=mid-1;
        }
        return low;
    }
    
```

补充一下对于经典的二分查找算法的解释： 
[知乎-二分查找有几种写法？它们的区别是什么？](https://www.zhihu.com/question/36132386/answer/155438728)
