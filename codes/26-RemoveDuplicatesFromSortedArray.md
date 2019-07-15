### 题目说明

Given a sorted array, remove the duplicates in-place such that each element appear only once and return the new length. 

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory. 

Example:

Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively. 

It doesn’t matter what you leave beyond the new length.

注意一下和27题和83题的对比。

### 代码

```
int removeDuplicates(vector<int>& nums) {
    int dup=0;
    for(int i=1;i<nums.size();i++){
    if(nums[i]==nums[i-1])
        dup++;
    else
        nums[i-dup]=nums[i];       
    }
    return nums.size()-dup;
}
```
