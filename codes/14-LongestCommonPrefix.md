### 问题描述

Write a function to find the longest common prefix string amongst an array of strings. 

If there is no common prefix, return an empty string “”. 

**Example 1**

  Input: [“flower”,”flow”,”flight”] 

Output: “fl”

**Example 2**

  Input: [“dog”,”racecar”,”car”] 
  
  Output: “” 
  
  Explanation: There is no common prefix among the input strings.


> Note:All given inputs are in lowercase letters a-z.



### 思路

把字符串数组的第一个字符串作为标准，其他字符串依次与第一个字符串的第一个、第二个、第三个…字母进行比较，一旦比较不成功，就返回之前所有已经比较成功的前缀作为最长前缀

代码如下：

```
string longestCommonPrefix(vector<string>& strs) {
        if(strs.empty())
            return "";
        for(int i=0;i<strs[0].length();i++){
            for(int j=1;j<strs.size();j++){
                if(strs[j][i]!=strs[0][i])
                    return strs[0].substr(0,i);
            }
        } 
        return strs[0];
    }
```
