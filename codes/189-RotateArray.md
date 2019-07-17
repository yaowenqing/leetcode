### 问题描述

Rotate an array of n elements to the right by k steps. 

For example, with n = 7 and k = 3, the array [1,2,3,4,5,6,7] is rotated to [5,6,7,1,2,3,4].  

with n = 7 and k = 2, the array [1,2,3,4,5,6,7] is rotated to [6,7,1,2,3,4,5]. 

>Note: Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem. 

最开始遇到了一些波折，因为我默认k是小于等于nums.size()的数字，但是submit的时候出错了。事实上，k可以大于nums.size()，所以我对k做了模n的操作，然后成功了。 

### 代码：

```
void rotate(vector<int>& nums, int k) {
        vector <int> nums2=nums;
        int n=nums.size();
        k=k%n;
        for(int i=0;i<n;i++){
            if(i<k)
                nums[i]=nums2[n-k+i];
            else
                nums[i]=nums2[i-k];
        }
    }
```   
 
事实上，

```
if(i<k)
    nums[i]=nums2[n-k+i];
else
    nums[i]=nums2[i-k];
```

这段代码可以换成

```
nums[(i + k)%n] = nums2[i];
```
