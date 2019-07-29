You’re given a matrix represented by a two-dimensional array, and two positive integers r and c representing the row number and column number of the wanted reshaped matrix, respectively. 

The reshaped matrix need to be filled with all the elements of the original matrix in the same row-traversing order as they were.  

If the ‘reshape’ operation with given parameters is possible and legal, output the new reshaped matrix; Otherwise, output the original matrix. 

**Example 1**

  Input:  
 
 nums =  
 
 [[1,2], 
 
 [3,4]] 
 
 r = 1, c = 4 
 
 Output:  
 
 [[1,2,3,4]] 
 
 Explanation: 
 
 The row-traversing of nums is [1,2,3,4]. The new reshaped matrix is a 1 * 4 matrix, fill it row by row by using the previous list.

**Example 2**

  Input:  
  
  nums =  
  
  [[1,2], 
  
  [3,4]] 
  
  r = 2, c = 4 
  
  Output:  
  
  [[1,2], 
  
  [3,4]] 
  
  Explanation: 
  
  There is no way to reshape a 2 * 2 matrix to a 2 * 4 matrix. So output the original matrix.

Note:


- The height and width of the given matrix is in range [1, 100]. 
- The given r and c are all positive.


### 关于vector的一些知识。 

初始化二维vector，为r×c的vector，所有值为0的方法：  

直接用初始化的方法：

```
vector<vector<int>> newOne(r,vector<int>(c,0));
```

用resize()来控制大小：

```
vector<vector<int>>res;
res.resize(r);//r行
for(int k=0;k<r;k++)
    res[k].resize(c);//每行为c列
```


### 代码


```
vector<vector<int>> matrixReshape(vector<vector<int>>& nums, int r, int c) {
        int m=nums.size(),n=nums[0].size();
        if(m*n!=r*c){
            return nums;
        }
        vector<vector<int> >res;
        res.resize(r);//r行
        for(int k = 0; k < r; ++k){
            res[k].resize(c);//每行为c列
        }
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                int k=i*n+j;
                res[k/c][k%c]=nums[i][j];
            }
        }
        return res;
    }
```
