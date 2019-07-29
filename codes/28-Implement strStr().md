Implement strStr().

Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

**Example 1**

  Input: haystack = “hello”, needle = “ll” 

 Output: 2

**Example 2**

  Input: haystack = “aaaaa”, needle = “bba” 
  
  Output: -1

Clarification:

What should we return when needle is an empty string? This is a great question to ask during an interview.For the purpose of this problem, we will return 0 when needle is an empty string. This is consistent to C’s strstr() and Java’s indexOf().


### 代码

```
int strStr(string haystack, string needle) {
        if(needle.length()==0)
            return 0;
        int n=haystack.length();
        int k=needle.length();       
        for(int i=0;i<=n-k;i++){
            int offset=0;
            while(haystack[i+offset]==needle[offset]&&offset<=k-1){
                offset++;
            }
            if(offset==k)
                return i;
        }
        return -1;
    }
```
