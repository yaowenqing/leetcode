Given an m x n matrix. If an element is 0, set its entire row and column to 0. Do it in-place.

Follow up:

- A straight forward solution using O(mn) space is probably a bad idea.
- A simple improvement uses O(m + n) space, but still not the best solution.
- Could you devise a constant space solution?

比较容易想到的办法：用两个boolean数组来维护之前矩阵为0的位置，然后更换矩阵元素。空间复杂度为O(m+n)

```java
class Solution {
    public void setZeroes(int[][] matrix) {
        int m=matrix.length;
        int n=matrix[0].length;
        boolean[] row=new boolean[m];
        boolean[] col=new boolean[n];
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(matrix[i][j]==0){
                    row[i]=true;
                    col[j]=true;
                }
            }
        }
        for(int i=0;i<m;i++){
            if(row[i]){
                for(int j=0;j<n;j++){
                    matrix[i][j]=0;
                }
            }
        }
        for(int j=0;j<n;j++){
            if(col[j]){
                for(int i=0;i<m;i++){
                    matrix[i][j]=0;
                }
            }
        }
    }
}
```

一个空间复杂度为O(1)的方法：

1.找到一个全不为0的noZeroRow行，用这个行来记录每个列是否有零。

2.把所有有0的行的所有元素置为0。（除了noZeroRow行）

3.再把noZeroRow行所有0对应的列所有元素置为0。

**(即用这个noZeroRow行完成了之前两个boolean数组的功能，不需要额外的空间)**

```java
class Solution {
    public void setZeroes(int[][] matrix) {

        int noZeroRow=-1;//标记全不为0的行
        int m=matrix.length;
        int n=matrix[0].length;

        for(int i=0;i<m;i++){
            int j=0;
            for(;j<n;j++){
                if(matrix[i][j]==0)
                    break;
            }
            if(j==n)//如果遍历到了最后仍然没有发现0，说明这一行全不为0
                noZeroRow=i;
        }

        if(noZeroRow==-1){//说明每一行都有0，整个矩阵赋为0
            for(int i=0;i<m;i++){
                for(int j=0;j<n;j++){
                    matrix[i][j]=0;
                }
            }
        }else{//用这不为0的行来记录所有存在0的列
            for(int i=0;i<m;i++){
               for(int j=0;j<n;j++){
                   if(matrix[i][j]==0)
                       matrix[noZeroRow][j]=0;
                }
            }
            for(int i=0;i<m;i++){
                //跳过noZeroRow行
                if(i==noZeroRow)
                    continue;
                for(int j=0;j<n;j++){
                    if(matrix[i][j]==0){
                        for(int j2=0;j2<n;j2++){
                            //把存在0的行的所有数置为0
                            matrix[i][j2]=0;
                        }
                    }
                }
            }
            for(int j=0;j<n;j++){
                //noZeroRow记录下来原本存在0的列，现在把这些列全置为0
                if(matrix[noZeroRow][j]==0){
                    for(int i=0;i<m;i++){
                        matrix[i][j]=0;
                    }
                }
            }
        }
    }
}
```
