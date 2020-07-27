Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

- Note: You can only move either down or right at any point in time.

Example:

>Input:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]

>Output: 7

>Explanation: Because the path 1→3→1→1→1 minimizes the sum.

用动态规划的方法，创建一个res数组，数组中每个元素代表的意义是从左上角到这个位置的最短路径。最后返回res数组右下的值。

动态规划转移方程：到该位置的最短路径=该位置的数字+min（到该位置上面元素的最短路径，到该位置左边元素的最短路径）

```java
class Solution {
    public int minPathSum(int[][] grid) {
        int m=grid.length;
        int n=grid[0].length;
        int res[][]=new int[m][n];
        int temp=0;
        
        for(int i=0;i<m;i++){
            res[i][0]=grid[i][0]+temp;
            temp+=grid[i][0];
        }
        temp=grid[0][0];
        for(int j=1;j<n;j++){
            res[0][j]=grid[0][j]+temp;
            temp+=grid[0][j];
        }
        
        for(int i=1;i<m;i++){       
            for(int j=1;j<n;j++){               
                res[i][j]=grid[i][j]+Math.min(res[i-1][j],res[i][j-1]);
            }
        }
        return res[m-1][n-1];
    }
}
```
