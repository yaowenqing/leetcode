### 题目描述

Given an array of integers, find out whether there are two distinct indices i and j in the array such that the absolute difference between nums[i] and nums[j] is at most t and the absolute difference between i and j is at most k.

**Example 1**

Input: nums = [1,2,3,1], k = 3, t = 0

Output: true

**Example 2**

Input: nums = [1,0,1,1], k = 1, t = 2

Output: true

**Example 3**

Input: nums = [1,5,9,1,5,9], k = 2, t = 3

Output: false

### 思路

和第219题一样，且始终保持所处理集合部分中的元素在k个以内，一旦超过k，就删除前面的元素，这样保证了不会有下标距离之差大于k的元素。

这里我们使用map数据结构来求解，map用来记录数字和其下标之间的映射。需要两个指针i和j，刚开始i和j都指向0，然后i开始向右走遍历数组，如果i和j之差大于k，且m中有nums[j]，则删除前面的元素，即给j加一，这样保证了m中的所有数的下标之差都不大于k。

之后我们用map数据结构的lower_bound()函数来找一个特定范围，就是大于或等于nums[i]-t的地方，所有小于这个阈值的数和nums[i]的差的绝对值会大于t。然后检测后面的所有的数字，如果数的差的绝对值小于等于t就返回true，最后遍历完整个数组返回false。

代码如下：

```
bool containsNearbyAlmostDuplicate(vector<int>& nums, int k, int t) {
        map<long long,int>m;
        int j=0;
        for(int i=0;i<nums.size();i++){
            if(i-j>k)
                m.erase(nums[j++]);
            auto a=m.lower_bound((long long)nums[i]-t);
            if(a!=m.end()&&abs(a->first-nums[i])<=t)
                return true;
            m[nums[i]]=i;
        }
        return false;     
    }
```
