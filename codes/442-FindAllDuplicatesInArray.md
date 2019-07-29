Given an array of integers, 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once. 

Find all the elements that appear twice in this array. 

Could you do it without extra space and in O(n) runtime?

** Example **

input:[4,3,2,7,8,2,3,1]

output:[2,3]

### 思路

在O(n)的时间复杂度内解决问题，不借助多余的空间。主要思路是把数组中的每一个元素的值映射成为所在的位数。比如for循环从0开始，第一个元素的值是4，所以映射成为原来的数组中的第4个数，也就是nums[3]（所以还要减1）。然后把nums[3]变为nums[3]的相反数。这就要求在之前映射的过程中有一个取绝对值的操作。如果第4个数num[3]已经是负数了，说明对nums[3]之前已经进行过一次操作了，说明数字4是重复的。在结果数组中push_back数字4。以此类推。

```
vector<int> findDuplicates(vector<int>& nums) {
        vector<int>res;
        for(int i=0;i<nums.size();i++){
            int index=abs(nums[i])-1;
            if(nums[index]<0)
                res.push_back(abs(nums[i]));
            nums[index]=-nums[index];
        }
        return res;
    }


```
