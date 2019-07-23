### 问题描述

Given an array nums, write a function to move all 0’s to the end of it while maintaining the relative order of the non-zero elements.

**Example**

Input: [0,1,0,3,12]

Output: [1,3,12,0,0]

Note:

- You must do this in-place without making a copy of the array.

- Minimize the total number of operations.

### 代码

第一次提交的

```
void moveZeroes(vector<int>& nums) {
        int times=0,signal=0;
        int n=nums.size();
        for(int i=0;i<n;i++){
            if(nums[i]==0)
                times++;
        }
        for(int i=0;i<n;i++){
           if(nums[i]!=0)
               nums[signal++]=nums[i];                           
        }
        for(int j=n-times;j<n;j++){
            nums[j]=0;
        }
    }
```

稍微简化了一下又提交了一次：

```
void moveZeroes(vector<int>& nums) {
        int signal=0;
        int n=nums.size();
        for(int i=0;i<n;i++){
           if(nums[i]!=0)
               nums[signal++]=nums[i];                           
        } 
        for(int j=signal;j<n;j++){
            nums[j]=0;
        }
    }
```

网上看到的另外一个有趣的方法：用替换法in-place来做，需要用两个指针，一个不停的向后扫，找到非零位置，然后和前面那个指针交换位置即可

```
void moveZeroes(vector<int>& nums) {
        for (int i = 0, j = 0; i < nums.size(); ++i) {
            if (nums[i]) {
                swap(nums[i], nums[j++]);
            }
        }
    }
```
