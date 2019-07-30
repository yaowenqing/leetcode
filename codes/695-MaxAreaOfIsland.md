Given a non-empty 2D array grid of 0’s and 1’s, an island is a group of 1’s (representing land) connected 4-directionally (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

Find the maximum area of an island in the given 2D array. (If there is no island, the maximum area is 0.)  

**Example 1**


  [[0,0,1,0,0,0,0,1,0,0,0,0,0], 
  
   [0,0,0,0,0,0,0,1,1,1,0,0,0], 
   
   [0,1,1,0,1,0,0,0,0,0,0,0,0], 
   
   [0,1,0,0,1,1,0,0,1,0,1,0,0], 
   
   [0,1,0,0,1,1,0,0,1,1,1,0,0], 
   
   [0,0,0,0,0,0,0,0,0,0,1,0,0], 
   
   [0,0,0,0,0,0,0,1,1,1,0,0,0], 
   
   [0,0,0,0,0,0,0,1,1,0,0,0,0]]


Given the above grid, return 6. Note the answer is not 11, because the island must be connected 4-directionally. 

**Example 2**


  [[0,0,0,0,0,0,0,0]]


Given the above grid, return 0. 

> Note: The length of each dimension in the given grid does not exceed 50. 

### 思路

采用DFS深度优先搜索算法，深搜每个非0点的最大连通区域的值，已经被遍历过的点要被标记为0。

这行代码

```
if(i>=0 && i<grid.size() && j>=0 && j<grid[0].size() && grid[i][j]==1)1
```

的目的是防止在+1和-1的过程中出现数组越界的情况。

代码：

```
int maxAreaOfIsland(vector<vector<int>>& grid) {
        int max_area=0;
        for(int i=0;i<grid.size();i++)
            for(int j=0;j<grid[0].size();j++)
                if(grid[i][j]==1)
                    max_area=max(max_area,AreaOfIsland(grid,i,j));
        return max_area;
    }

    int AreaOfIsland(vector<vector<int>>& grid,int i,int j){
        if(i>=0 && i<grid.size() && j>=0 && j<grid[0].size() && grid[i][j]==1){
            grid[i][j]=0;
            return 1 + AreaOfIsland(grid,i+1,j)+AreaOfIsland(grid,i-1,j)+AreaOfIsland(grid,i,j-1)+AreaOfIsland(grid,i,j+1);
        }
        return 0;
    }
```
