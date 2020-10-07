Given an array with n objects colored red, white or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

Note: You are not suppose to use the library's sort function for this problem.

**Example**

Input: [2,0,2,1,1,0]

Output: [0,0,1,1,2,2]

Follow up:
- 一个直观的解决方案是使用计数排序的两趟扫描算法。首先，迭代计算出0、1 和 2 元素的个数，然后按照0、1、2的排序，重写当前数组。
- 你能想出一个仅使用常数空间的一趟扫描算法吗？

两次遍历数组的方法：

```C++
void sortColors(vector<int>& nums) {
        vector <int>color(3);
        for(int num:nums)
            color[num]++;
        for(int i=0,cur=0;i<3;i++){
            for(int j=0;j<color[i];j++){
                nums[cur++]=i;       
            }
        }
}
```

一次遍历数组的方法：用两个指针，分别从数组的首部和尾部往中心移动。

zero指针指向开头的位置，two指针指向末尾的位置。

从头遍历数组，如果遇到0，交换该值和zero指针指向的值，并将zero指针后移；

如果遇到2，就交换该值和two指针指向的值，并将two指针前移，同时还需要再对交换后的该位置进行一次判断（因为可能换过来的还需要和zero指针交换一次）；

如果遇到1就继续向前遍历

```C++
void sortColors(vector<int>& nums) {
        int zero=0,two=nums.size()-1;
        for(int i=0;i<=two;i++){
            if(nums[i]==0)
                swap(nums[i],nums[zero++]);
            else if(nums[i]==2)
                swap(nums[i--],nums[two--]);
        }
    }
```   

Java方法：
```
class Solution {
    public void sortColors(int[] nums) {
        int num0=0;
        int num1=0;
        int num2=0;
        for(int i=0;i<nums.length;i++){
            if(nums[i]==0)
                num0++;
            if(nums[i]==1)
                num1++;
            if(nums[i]==2)
                num2++;
        }
        for(int i=0;i<nums.length;i++){
            if(num0-->0){
                nums[i]=0;
            }else if(num1-->0){
                nums[i]=1;
            }else{
                nums[i]=2;
            }
        }
    }
}
```
