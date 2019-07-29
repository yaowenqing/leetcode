### 问题描述

Given an array of integers sorted in ascending order, find the starting and ending position of a given target value. 

Your algorithm’s runtime complexity must be in the order of O(log n). 

If the target is not found in the array, return [-1, -1]. 

For example, 

Given [5, 7, 7, 8, 8, 10] and target value 8, 

return [3, 4].  

Given [5, 7, 7, 8, 10] and target value 8, 

return [3, 3]. 

### 解题思路

我的思路是用二分查找的办法先找到等于target的位置，然后扩展这个位置，找到这个位置附近所有等于target的其他位置，然后定位起始点和终点。

```
vector<int> searchRange(vector<int>& nums, int target) {
        vector<int> res;
        int n=nums.size();
        if(n==0){ //如果为空就直接返回[-1,-1]
            res.push_back(-1);
            res.push_back(-1);
            return res;
        }                
        int a=0,b=n-1;
        while(a<=b){
            int c=a+(b-a)/2;
            cout<<c<<endl;
            if(nums[c]<target) a=c+1;         
            else if(nums[c]>target) b=c-1;//二分查找的基本思路
            else if(nums[c]==target){//找到了target的位置
                int d=c;
                while(nums[c]==target) {
                    c--; 
                    if(c<0) break;
                }                                
                a=c+1;
                while(nums[d]==target) d++;
                b=d-1;
                res.push_back(a);
                res.push_back(b);
                return res;
            }
        }   
        //没有找到target，返回[-1,-1]
        res.push_back(-1);
        res.push_back(-1);
        return res;
    }
```

在网上看到的一个更简洁的解法如下：


```
vector<int> searchRange(vector<int>& nums, int target) {
        int idx1 = lower_bound(nums, target);
        int idx2 = lower_bound(nums, target+1)-1;
        if (idx1 < nums.size() && nums[idx1] == target)
            return {idx1, idx2};
        else
            return {-1, -1};
    }

    int lower_bound(vector<int>& nums, int target) {
        int l = 0, r = nums.size()-1;
        while (l <= r) {
            int mid = (r-l)/2+l;
            if (nums[mid] < target)
                l = mid+1;
            else
                r = mid-1;
        }
        return l;
    }
```

lower_bound函数相当于完成了二分查找的功能 

二分查找算法推广到有重复元素的空间，就成为了→寻找该元素第一次出现的位置


也可以理解成为→寻找第一个大于等于目标值的元素位置


那么这个算法首先对target用lower_bound函数，即找到了target第一个出现的位置；对target+1用lower_bound函数，即找到了大于等于target的元素第一个出现的位置，减去1即为target最后出现的位置。
