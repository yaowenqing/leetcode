### 题目描述

Given an array of 2n integers, your task is to group these integers into n pairs of integer, say (a1, b1), (a2, b2), …, (an, bn) which makes sum of min(ai, bi) for all i from 1 to n as large as possible.  

**Example 1**


  Input: [1,4,3,2] 
  
  Output: 4 
  
  Explanation: n is 2, and the maximum sum of pairs is 4 = min(1, 2) + min(3, 4).


Note:


  - n is a positive integer, which is in the range of [1, 10000]. 
  - All the integers in the array will be in the range of [-10000, 10000].

### 代码

思路是从把数组里的元素从小到大排序。然后取出数组里面的所有第奇数个元素，相加并返回相加得到的结果。

```
int arrayPairSum(vector<int>& nums) {
        for(int i=0;i<nums.size()-1;i++){
            for(int j=i+1;j<nums.size();j++){
                if(nums[i]>nums[j]){
                    int k=nums[i];
                    nums[i]=nums[j];
                    nums[j]=k;
                }
            }
        }
        int sum=0;
        for(int m=0;m<nums.size();m++){
            if(m%2==0)
                sum=sum+nums[m];
        }
        return sum;
    }
```

但是超时了，于是在相同思路的情况下稍微调整一下代码（主要是简化了排序的过程，在for循环中去除了模2的判断条件并把步长改为2），这次成功了：



```
int arrayPairSum(vector<int>& nums) {
    int sum = 0;
    sort(nums.begin(), nums.end());
    for (int i = 0; i < nums.size(); i += 2) {
        sum += nums[i];
    }
    return sum;
}
```
