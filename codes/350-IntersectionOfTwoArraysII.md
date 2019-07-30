Given two arrays, write a function to compute their intersection.

**Example 1**

Input: nums1 = [1,2,2,1], nums2 = [2,2]

Output: [2,2]

**Example 2**

Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]

Output: [4,9]

Note:
- Each element in the result should appear as many times as it shows in both arrays. 
- The result can be in any order. 

Follow up:
- What if the given array is already sorted? How would you optimize your algorithm? 
- What if nums1's size is small compared to nums2's size? Which algorithm is better? 
- What if elements of nums2 are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?

### 思路

用哈希表来建立nums1中字符和其出现个数之间的映射, 然后遍历nums2数组，如果当前字符在哈希表中的个数大于0，则将此字符加入结果res中，然后哈希表该字符对应的出现次数自减1

```
vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        unordered_map<int,int>m;
        vector<int> res;
        for(auto a:nums1)
            m[a]++;
        for(auto a:nums2)
            if(m[a]-->0)
                res.push_back(a);
        return res;  
    }
```

在提示信息中有提到如果两个数组已经是有序数组了是否可以优化算法，所以在代码中加入排序的部分，然后用两个指针分别指向两个数组的起始位置，如果两个指针指的数字相等，则存入结果中，两个指针均自增1，如果第一个指针指的数字大，则第二个指针自增1，反之亦然，代码如下：

```
vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        vector<int> res;
        int i = 0, j = 0; //两个跟踪数组的指针
        sort(nums1.begin(), nums1.end());
        sort(nums2.begin(), nums2.end());
        while(i<nums1.size()&&j<nums2.size()){
            if(nums1[i]==nums2[j]){
                res.push_back(nums1[i]);
                i++;
                j++;
            }else if(nums1[i]<nums2[j]){
                i++;
            }else{
                j++;
            }            
        }
        return res;
    }
```
