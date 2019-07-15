### 问题描述

Given numRows, generate the first numRows of Pascal’s triangle. 

For example, given numRows = 5,

Return  

[ 

   [1], 
     
   [1,1], 
    
   [1,2,1], 
   
  [1,3,3,1], 
  
 [1,4,6,4,1] 
 
] 

### 代码

```
vector<vector<int>> generate(int numRows) {
        vector<vector<int>> res(numRows);
        if(numRows==0){
            return res;
        }
        res[0].push_back(1);
        for(int i=1;i<numRows;i++){
            res[i].push_back(1);
            for(int j=1;j<i;j++){             
                res[i].push_back(res[i-1][j-1]+res[i-1][j]);                
            }
            res[i].push_back(1);
        }
        return res;
}
```
