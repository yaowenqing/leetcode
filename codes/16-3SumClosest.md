Given an array nums of n integers and an integer target, find three integers in nums such that the sum is closest to target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

 

- Example 1:
- Input: nums = [-1,2,1,-4], target = 1
- Output: 2
- Explanation: The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).

和15题很类似，用三指针的方法。

每次循环中如果三数之和更接近target就更新res的值，然后移动指针，每次只移动一个指针。


```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);
        int res=nums[0]+nums[1]+nums[2];
        
        for(int start=0;start<nums.length-2;start++){
            int middle=start+1;
            int end=nums.length-1;
            
            while(middle<end){                
                int sum=nums[start]+nums[middle]+nums[end];                
                if(Math.abs(sum-target)<Math.abs(res-target))
                    res=sum;
                if(sum==target){
                    return target;
                }else if(sum<target){
                    middle++;
                }else{
                    end--;
                }                   
            }
            
        }     
        return res;        
    }
}
```
