### 问题描述

Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array. 

>Note: You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2. The number of elements initialized in nums1 and nums2 are m and n respectively. 

### 第一次提交的代码

```
void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
    int i=m-1,j=n-1,all=m+n-1;
    while(all--){
        nums1[all]=(nums1[i]>nums2[j]&&i>=0)?nums1[i--]:nums2[j--];
    }
}
```

上面是我第一次提交的代码，但是Submission Result: Runtime Error  

仔细分析一下可以发现问题所在。 

如果nums1=[1,2,3],nums2=[] 

按照这段代码，第一次循环中会对nums1[2]和nums2[-1]进行比较，这显示不正确的。 

事实上，如果第二个数组是空的，那就没有必要考虑第二个数组，直接把第一个数组当作最终结果就行了。因此我们while循环的判断条件以第二个数组是否为空进行判断

### 代码修改为如下

```
void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
    int i=m-1,j=n-1,all=m+n-1;
    while(j>=0){
        nums1[all--]=(nums1[i]>nums2[j]&&i>=0)?nums1[i--]:nums2[j--];
    }
}
```

这次成功了。
