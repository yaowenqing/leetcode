### 题目

Give a string s, count the number of non-empty (contiguous) substrings that have the same number of 0’s and 1’s, and all the 0’s and all the 1’s in these substrings are grouped consecutively.  
Substrings that occur multiple times are counted the number of times they occur. 

**Example 1**

  Input: “00110011” 
  
  Output: 6 
  
  Explanation: There are 6 substrings that have equal number of consecutive 1’s and 0’s: “0011”, “01”, “1100”, “10”, “0011”, and “01”.


Notice that some of these substrings repeat and are counted the number of times they occur.

Also, “00110011” is not a valid substring because all the 0’s (and 1’s) are not grouped together.

**Example 2**

  Input: “10101” 
  
  Output: 4 
  
  Explanation: There are 4 substrings: “10”, “01”, “10”, “01” that have equal number of consecutive 1’s and 0’s.


Note: 

- s.length will be between 1 and 50,000. 
- s will only consist of “0” or “1” characters.

### 解题思路

创建一个数组，这个数组用来存储所有连续的1和连续的0的个数，例如”111001111”字符串对应到这个数组存储的元素就是”3 2 4”，然后依次比较这个数组中相邻两个数，获得那个较小的数字。把数组中n个元素中n-1个比较出来得到最小数加在一起，就是最后的结果。 
这是因为在连续的m个0紧接着连续的n个1形成的字符串中，可以形成的符合要求的子串个数共有min(m,n)个。 

以111001111为例：11100可以形成min(3,2)=2个符合要求的子串，001111可以形成min(2,4)=2个符合要求的子串，所以共有4个符合要求的子串。

### 代码

```
int countBinarySubstrings(string s) {
        vector<int>consecutiveNo;
        int n=s.size();
        int count=1;
        for(int i=1;i<=n;i++){
            if(s[i]==s[i-1]){
                count++;
            }else{
                consecutiveNo.push_back(count);
                count=1;
            }
        }
        int res=0;
        for(int j=1;j<consecutiveNo.size();j++){
            res+=min(consecutiveNo[j],consecutiveNo[j-1]);
        }
        return res;
    }
```
