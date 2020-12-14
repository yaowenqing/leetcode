Suppose you have a long flowerbed in which some of the plots are planted and some are not. However, flowers cannot be planted in adjacent plots - they would compete for water and both would die.

Given a flowerbed (represented as an array containing 0 and 1, where 0 means empty and 1 means not empty), and a number n, return if n new flowers can be planted in it without violating the no-adjacent-flowers rule.

>Example 1:
Input: flowerbed = [1,0,0,0,1], n = 1
Output: True

>Example 2:
Input: flowerbed = [1,0,0,0,1], n = 2
Output: False

Note:
- The input array won't violate no-adjacent-flowers rule.
- The input array size is in the range of [1, 20000].
- n is a non-negative integer which won't exceed the input array size.

最简单的逻辑，一个一个地方扫过去看能不能摆放，如果可以摆放就把这个地方从0变为1。每次循环都比较一次已经摆的数目是否超过了n，可以提前终止，减少冗余。

代码：

```java
class Solution {
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        int k=flowerbed.length;
        int i=0;
        int max=0;
        while(i<k){
            if(flowerbed[i]==0 && (i==0||flowerbed[i-1]==0) &&
               (i==k-1||flowerbed[i+1]==0)){
                flowerbed[i]=1;
                max++; 
            }   
            if(max>=n)
                return true;
            i++;
        }
        return false;
    }
}
```

一个go语言版本：
```go
func canPlaceFlowers(flowerbed []int, n int) bool {
    for i :=0 ;i< len(flowerbed);i++ {
        if flowerbed[i] == 0 {
            if i == 0 || flowerbed[i-1] == 0 {
                flowerbed[i] = 1
                n--
            }
        }  else {
            if i != 0 && flowerbed[i-1] != 0{
                flowerbed[i-1] = 0
                n++
            }
        }
    }
    if n>0 {
        return false
    } else {
        return true
    }
}
```
