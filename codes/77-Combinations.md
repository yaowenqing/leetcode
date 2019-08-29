Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

**Example**

Input: n = 4, k = 2

Output:

[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]

一个比较朴素的算法
```
 vector<vector<int>> combine(int n, int k) {
        vector<vector<int>> res;
        vector<int>p(k,0);
        int i=0;
        while(i>=0){
            p[i]++;
            if(p[i]>n)
                i--;
            else if(i==(k-1))
                res.push_back(p);
            else{
                i++;
                p[i]=p[i-1];
            }
        }
        return res;
    }
```
