A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and empty space is marked as 1 and 0 respectively in the grid.

Note: m and n will be at most 100.

**Example 1**

Input:[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]

Output: 2

Explanation:

There is one obstacle in the middle of the 3x3 grid above.

There are two ways to reach the bottom-right corner:

1. Right -> Right -> Down -> Down

2. Down -> Down -> Right -> Right

简单明了的动态规划，先初始化第一行和第一列，和62题的区别在于如果遇到障碍直接把dp数组在障碍处设为0.

```C++
int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int m=obstacleGrid.size();
        int n=obstacleGrid[0].size();
        long int dp[m][n];
        int signal=1;
        for(int i=0;i<n;i++){
            if(obstacleGrid[0][i]==1)
                signal=0;
            if(signal==0)
                dp[0][i]=0;
            else
                dp[0][i]=1;
        }
        signal=1;
        for(int j=0;j<m;j++){
            if(obstacleGrid[j][0]==1)
                signal=0;
            if(signal==0)
                dp[j][0]=0;
            else
                dp[j][0]=1;
        }
        for(int i=1;i<m;i++){
            for(int j=1;j<n;j++){
                if(obstacleGrid[i][j]==1)
                    dp[i][j]=0;
                else
                    dp[i][j]=dp[i-1][j]+dp[i][j-1];
            }
        }
        return dp[m-1][n-1];
    }
```

上面是几年前用C++写的，空间复杂度也没有优化，下面是用java写的优化过空间复杂度的代码：
```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int m=obstacleGrid.length;
        int n=obstacleGrid[0].length;
        int []dp=new int[n];
        for(int j=0;j<n;j++){
            if(obstacleGrid[0][j]==1)
                break;
            dp[j]=1;
        }
        for(int i=1;i<m;i++){
            dp[0]=(obstacleGrid[i][0]==0 && dp[0]==1)?1:0;
            for(int j=1;j<n;j++){
                if(obstacleGrid[i][j]==1)
                    dp[j]=0;
                else{
                    dp[j]=dp[j]+dp[j-1];
                }
            }
        }
        return dp[n-1];
    }
}
```
