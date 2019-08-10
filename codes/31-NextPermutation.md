Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be in-place and use only constant extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.

1,2,3 → 1,3,2

3,2,1 → 1,2,3

1,1,5 → 1,5,1

# 实现原理

1：从右往左找到第一个比右边小的数，记录其位置为m;

2：再从右往左找到比m位置大的数中最小的一个，记录其位置为n

3：然后交换m,n位置的数

4：对m之后的位置，进行升序排列

代码：

```

void nextPermutation(vector<int>& nums) {
        int i=nums.size()-1;         
        for(;i>0;i--){
            if(nums[i]>nums[i-1])
                break;
        }
        if(i==0){
            sort(nums.begin(),nums.end());
            return;
        }
        int j=nums.size()-1;
        for(;j>=i;j--){
            if(nums[j]>nums[i-1]){
                swap(nums[i-1],nums[j]);
                break;
            }
        }
        sort(nums.begin()+i,nums.end());
}

```
