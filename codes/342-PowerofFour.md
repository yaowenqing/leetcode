注意强制类型转换，防止精度的损失。

```java
class Solution {
    public boolean isPowerOfFour(int num) {
        double a=(double)num;
        return isPowerOfFour(a);
    }
    public boolean isPowerOfFour(double num) {
        if(num==1.0)
            return true;
        if(num<1)
            return false;
        double n=num/4;
        return isPowerOfFour(n);
    }
}
```

非递归的解法：
```java
class Solution {
    public boolean isPowerOfFour(int num) {
        double a=(double)num;
        while(a>1.0){
            a/=4;
        }
        if(a==1.0)
            return true;
        else
            return false;
    }
}
```

非递归非循环的解法：(位运算)

```java
class Solution {
    public boolean isPowerOfFour(int num) {
        if(num<=0)
            return false;
        return (num & num-1)==0 && (num&0x55555555)==num; 
    }
}
```
