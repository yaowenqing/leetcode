## 题目说明

Given an array and a value, remove all instances of that value in-place and return the new length.  

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory. 

The order of elements can be changed. It doesn’t matter what you leave beyond the new length.

Example:

Given nums = [3,2,2,3], val = 3,

返回一个int类型的整数N，并使得原数组的前N位是所需要的数字。 
该例子应该返回整数2，代表数组的前两位是所需要的数字，此时的数组为[2,2]。 
和26题的基本思路是一致的。

### 代码

```C++
int removeElement(vector<int>& nums, int val) {
        int sign=0;
        for(int i=0;i<nums.size();i++){
            if(nums[i]==val)
                sign++;
            else
                nums[i-sign]=nums[i];
        }
        return nums.size()-sign;
    }
```

### JAVA
```java
public int removeElement(int[] nums, int val) {
        int k=0;
        for(int i=0;i<nums.length;i++){
            if(nums[i]!=val)
                nums[k++]=nums[i];
        }
        return k;
    }
```
