Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

**Example 1**

Input:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]

Output: [1,2,3,6,9,8,7,4,5]

**Example 2**

Input:
[
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9,10,11,12]
]

Output: [1,2,3,4,8,12,11,10,9,5,6,7]

思路不难，在大循环里套四个小循环，但要注意边界条件，写起来要注意的细节比较多

```
vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector<int> res;
        if (matrix.empty() || matrix[0].empty()) 
            return res;
        int m=matrix.size();
        int n=matrix[0].size();
        int round=m>n ? (n + 1) / 2 : (m + 1) / 2;
        int p=m,q=n;
        for(int i=0;i<round;i++,q-=2,p-=2){
            for(int col=i;col<i+q;col++)
                res.push_back(matrix[i][col]);
            for(int row=i+1;row<i+p;row++)
                res.push_back(matrix[row][q+i-1]);
            if(q==1||p==1)
                break;
            for(int col=q+i-2;col>i-1;col--)
                res.push_back(matrix[i+p-1][col]);
            for(int row=i+p-2;row>i;row--)
                res.push_back(matrix[row][i]);
        }              
        return res;
    }
```
