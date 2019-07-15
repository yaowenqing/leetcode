### 问题描述

Given a non-negative integer represented as a non-empty array of digits, plus one to the integer. 

You may assume the integer do not contain any leading zero, except the number 0 itself. 

The digits are stored such that the most significant digit is at the head of the list. 

用一个数组来代表一个非负整数，对这个整数进行+1操作，得到的结果也用数组进行表示。这个题目有假设前提：数组里的数字都是在0-9范围内的。

### 思路

从数组后面开始遍历数组，如果遇到9，就立刻把这一位置为0。否则给这一位++。++操作之后就可以return了。但是如果之前的数组的每一位都是9，说明for循环结束还没有返回，此时把原数组首位置为1，并弹入一个0。 

### 代码

```
vector<int> plusOne(vector<int>& digits) {
        int n = digits.size();
        for (int i = n - 1; i >= 0; --i){
            if (digits[i] == 9){
                digits[i] = 0;
            }
            else{
                digits[i]++;
                return digits;
            }
        }
        digits[0]=1;
        digits.push_back(0);
        return digits;  
    }
```
