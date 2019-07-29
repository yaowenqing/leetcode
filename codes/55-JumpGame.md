Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index. 

Example 1:

  Input: [2,3,1,1,4] 
  
  Output: true 
  
  Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.


Example 2:

  Input: [3,2,1,0,4] 
  
  Output: false 
  
  Explanation: You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index.


### 思路 

遍历所有的点，用max表示从现在这个点以及现在这个点之前的所有点出发能走的最远的地方，然后再遍历到下一个点，若走不到下一个点就返回false。

### 代码

```
bool canJump(vector<int>& nums) {
        int max=0;
        for(int i=0;i<nums.size();i++){
            if(max<i)
                return false;
            max=(max>i+nums[i]?max:i+nums[i]);          
        }
       return true;
    }
```
