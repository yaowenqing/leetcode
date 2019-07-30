There is a list of sorted integers from 1 to n. Starting from left to right, remove the first number and every other number afterward until you reach the end of the list.

Repeat the previous step again, but this time from right to left, remove the right most number and every other number from the remaining numbers.

We keep repeating the steps again, alternating left to right and right to left, until a single number remains.

Find the last number that remains starting with a list of length n.

Example:

Input:

n = 9,

1 2 3 4 5 6 7 8 9

2 4 6 8

2 6

6

Output:

6

### 思路

用一个bool型变量left来表示遍历顺序，为true表示从左往右，为false表示从右往左遍历。当n为1时，不论从左往右还是从右往左都返回1。如果n大于1，且是从左往右的话，返回2倍的对n/2的从右往左的遍历；如果是从右往左的话，要分奇偶情况，如果n为奇数，返回2倍的对n/2的从左往右的遍历的值；如果n为偶数，返回2倍的对n/2的从左往右的遍历的值，再减去1。

例如：

1 2 3 4 5 6 7 8 9 return 2*(4,left=false)

1 2 3 4 return 2*(2,left=true)-1

1 2 return 2*(1,left=false)=2*1=2 

代码如下：

```
int lastRemaining(int n) {
        return elimi(n,true);
    }
    int elimi(int n,bool left){
        if(n==1)
            return 1;
        if(left==true)
            return 2*elimi(n/2,false);
        else{
            if(n%2==0)
                return 2*elimi(n/2,true)-1;
            else
                return 2*elimi(n/2,true);
        }
}  
```
