### 问题描述

Let’s call an array A a mountain if the following properties hold:

A.length >= 3

There exists some 0 < i < A.length - 1 such that A[0] < A[1] < … A[i-1] < A[i] > A[i+1] > … > A[A.length - 1]

Given an array that is definitely a mountain, return any i such that A[0] < A[1] < … A[i-1] < A[i] > A[i+1] > … > A[A.length - 1].

**Example 1**

  Input: [0,1,0] 
  
  Output: 1

**Example 2**

  Input: [0,2,1,0] 
  
  Output: 1

### 思路

二分查找

```
int peakIndexInMountainArray(vector<int>& A) {
        int left=0,right=A.size()-1;
        int res=left+(right-left)/2;
        while(left<=right){
            res=left+(right-left)/2;
            if(A[res]<A[res-1]){
                right=res-1;
            }else if(A[res]<A[res+1]){
                left=res+1;
            }else{
                break;
            }          
        }
        return res;
    }
```
