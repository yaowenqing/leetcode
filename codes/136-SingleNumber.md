### 题目

Given an array of integers, every element appears twice except for one. Find that single one. 

### 解题思路

位操作

0 ^ N = N 

N ^ N = 0 

So….. if N is the single number 

N1 ^ N1 ^ N2 ^ N2 ^…………..^ Nx ^ Nx ^ N 

= (N1^N1) ^ (N2^N2) ^…………..^ (Nx^Nx) ^ N 

= 0 ^ 0 ^ ……….^ 0 ^ N 

= N

### 代码

```
int singleNumber(vector<int>& nums) {
        if(nums == null || nums.length == 0){
              return 0;
        }
        int result = A[0];

        for(int i = 1; i < A.length; i++){
            result = result ^ A[i];
        }
        return result;
}
```
