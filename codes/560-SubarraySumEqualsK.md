Given an array of integers and an integer k, you need to find the total number of continuous subarrays whose sum equals to k.

**Example 1**

Input:nums = [1,1,1], k = 2

Output: 2

**Example 1**

Input:nums = [3,4,7,2,-3,1,4,2], k = 7

Output: 4(3+4;7;7+2-3+1;1+4+2)


暴力解法：（居然可以通过）
```C++
int subarraySum(vector<int>& nums, int k) {
        int n=nums.size();
        int res=0;
        for(int i=0;i<n;i++){
            int sum=nums[i];
            if(sum==k)
                res++;  
            for(int j=i+1;j<n;j++){
                sum+=nums[j];
                if(sum==k)
                    res++; 
            }               
        }
        return res;
}
```
hashmap解法：

下标从0到n-1遍历，需要两个指针，sum记录数组到当前位置的累加和，sum-k记录sum-k，sum-k指针永远要后于sum指针，一旦发现两个指针错位所指的元素相等，就给res增加，增加的数量是在这个下标之前所有的sum的个数。而实现这一点主要靠hashmap来存储，hashmap的意义是sum的个数。

举例，下图中，0和0（永远初始化的时候都有0）错位相等，自增1；第二个指针到7的时候又看到了之前的7，自增1；第二个指针再次到7看到了之前的7，自增1；第二个指针到13的时候看到了之前的13，自增1。

值得一提的是，如果第二个指针到14，那么就会自增2，因为它可以看到之前的2个14.

|i          |    0    |1|2|3|4|5|6|7|
|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|
|nums[i]    |  3  |4|7|2|-3|1|4|2|
|sum        |  3  |7|14|16|13|14|18|20| 
|sum-k      |  -4|0|7|9|6|7|11|13|
```C++
 int subarraySum(vector<int>& nums, int k) {
        int n=nums.size();
        int res=0,sum=0;
        unordered_map<int, int> m{{0, 1}};
        for(int i=0;i<n;i++){
            sum+=nums[i];
            res+=m[sum-k];
            m[sum]++;
        }
        return res;
    }
```
