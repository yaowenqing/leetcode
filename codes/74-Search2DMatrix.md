Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

- Integers in each row are sorted from left to right.
- The first integer of each row is greater than the last integer of the previous row.

>Example 1:

Input:

matrix = [

  [1,   3,  5,  7],

[10, 11, 16, 20],

[23, 30, 34, 50]

]

target = 3

Output: true

>Example 2:

Input:

matrix = [

[1,   3,  5,  7],

[10, 11, 16, 20],

[23, 30, 34, 50]

]

target = 13

Output: false

自己写的方法，直接用两次二分查找

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix.length==0||matrix[0].length==0)
            return false;
        int m=matrix.length;
        int n=matrix[0].length;
        
        //首先确定target所在行
        int start=0;
        int end=m-1;
        int targetRow=0;
        while(start<=end){
            int mid=(start+end)/2;   
            if(matrix[mid][0]>target)
                end=mid-1;
            else if(matrix[mid][n-1]<target)
                start=mid+1;
            else{
                targetRow=mid;
                break;
            }           
        }
        //对所在的这一行进行二分查找
        int left=0;
        int right=n-1;      
        while(left<=right){
            int mid=(left+right)/2;
            if(matrix[targetRow][mid]>target){
                right=mid-1;
            }else if(matrix[targetRow][mid]<target){
                left=mid+1;
            }else{
                return true;
            }           
        }
        return false;
    }
}
```

解法二：看到别人写的一个比较巧妙的办法，直接把二维数组转化为一维数组进行二分查找。关键点在于二维坐标和一维坐标之间的转换。

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix.length==0||matrix[0].length==0)
            return false;
        int m=matrix.length;
        int n=matrix[0].length;
        int left=0;
        int right=m*n-1;
        while(left<=right){
            int mid=(left+right)/2;
            if(matrix[mid/n][mid%n]==target)
                return true;
            if(matrix[mid/n][mid%n]<target)
                left=mid+1;
            else
                right=mid-1;
        }        
        return false;
    }
}
```

解法三：还可以用双指针法。逻辑很简单，看下面代码即可。

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix.length==0||matrix[0].length==0)
            return false;
        int i=0;
        int j=matrix[0].length-1;
        while(i<matrix.length && j>=0){
            if(matrix[i][j]==target)
                return true;
            else if(matrix[i][j]>target)
                j--;
            else
                i++;            
        }        
        return false;
    }
}
```
