### 题目描述

Given an array of integers that is already sorted in ascending order, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based. 

You may assume that each input would have exactly one solution and you may not use the same element twice.

Input: numbers={2, 7, 11, 15}, target=9

Output: index1=1, index2=2

### 代码

本题可以用leetcode第一题的方法，由于nums数组是sorted的，所以还可以用下面的方法：

```
vector<int> twoSum(vector<int>& nums, int target) {
        int left=0,right=nums.size()-1;       
        while(left<right){
            if(nums[left]+nums[right]==target){
                vector<int>result{left+1,right+1};
                return result;
            }
            else if(nums[left]+nums[right]<target){
                left++;
            }
            else
                right--;        
        }
    }

```
