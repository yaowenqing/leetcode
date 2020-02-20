Given an array of integers and an integer k, you need to find the total number of continuous subarrays whose sum equals to k.

**Example 1**

Input:nums = [1,1,1], k = 2

Output: 2

**Example 1**

Input:nums = [3,4,7,2,-3,1,4,2], k = 7

Output: 4(3+4;7;7+2-3+1;1+4+2)


暴力解法：（居然可以通过）
```
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
```
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
