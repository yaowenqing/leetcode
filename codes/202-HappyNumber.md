### 问题描述

Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

Example: 19 is a happy number

$1^{2}$ + $9^{2}$ = $82$

$8^{2}$+ $2^{2}$ = $68$

$6^{2}$ + $8^{2}$ = $100$

$1^{2}$+ $0^{2}$ + $0^{2}$ = $1$

##自己写的
思路是把数字的每个位置相加得到新数字，并放入check数组中，若已有这个数字，说明出现了循环，返回false。如果while循环中止，说明得到了1，是一个快乐数，返回true。

```
bool isHappy(int n) {
        int b=n,total=0;
        vector<int>check;
        while(b!=1){
            int c=b; 
            total=0;
            while(c!=0){
                total=total+pow(c-c/10*10,2);
			    c=c/10;
            }
            for(int i=0;i<check.size();i++){
                if(check[i]==total)
                    return false;
            }
            check.push_back(total);
            b=total;
        }
        return true;
    }
```
通过了但是太慢了，要85ms，下面这个方法只要3ms
##别人的方法
```
bool isHappy(int n) {
        int slow, fast;
        slow = fast = n;
        do{
            slow = digitSquareSum(slow);
            fast = digitSquareSum(fast);
            fast = digitSquareSum(fast);
        } while(slow != fast);
        if (slow == 1) return 1;
        else return 0;
    }
    int digitSquareSum(int n) {
        int sum = 0, tmp;
        while (n) {
            tmp = n % 10;
            sum += tmp * tmp;
            n /= 10;
        }
        return sum;
    }
```
isHappy还可以做下面的优化，减少fast==1时多余的等待
```
bool isHappy(int n) {
        int slow, fast;
        slow = fast = n;
        do {
            slow = digitSquareSum(slow);
            fast = digitSquareSum(fast);
            fast = digitSquareSum(fast);
            if(fast == 1) return 1;
        } while(slow != fast);
         return 0;
}
```


该方法基于的思想是Floyd判圈算法（龟兔赛跑算法） ，参考下面的博客：
[Floyd判圈算法（龟兔赛跑算法）](http://blog.csdn.net/xiaoquantouer/article/details/51620657)
#Floyd判圈算法（龟兔赛跑算法）
Floyd判圈算法（Floyd Cycle Detection Algorithm），又称龟兔赛跑算法（Tortoise and Hare Algorithm），是一个可以在有限状态机、迭代函数或者链表上判断是否存在环，以及判断环的起点与长度的算法。

**基本思路：**在某种关系下，顶点 i 到 k 拓扑有序，顶点 k 到 j 也是相同的顺序，那么 i 和 j 也存在这个顺序。要是某一个顶点出现了自己到自己的环，那么图中就有环，但是这种方法复杂度高一些，没有检测顶点出度或者DFS的方法快，但是非常简单。

**问题：**如何检测一个链表是否有环，如果有，那么如何确定环的起点和环的长度。

**解决方案：**
（1）判断是否有环？
龟兔解法的基本思想可以用我们跑步的例子来解释，如果两个人同时出发，如果赛道有环，那么快的一方总能追上慢的一方。进一步想，追上时快的一方肯定比慢的一方多跑了几圈，即多跑的路的长度是圈的长度的倍数。

基于上面的想法，Floyd用两个指针，一个慢指针（龟）每次前进一步，快指针（兔）指针每次前进两步（两步或多步效果时等价的，只要一个比另一个快就行）。如果两者在链表头以外的某一点相遇（即相等）了，那么说明链表有环，否则，如果（快指针）到达了链表的结尾，那么说明没坏。

（2）求环的长度
相遇的时候，一定已经在环上了，然后两个人只要再次在环上接着跑，再次相遇的时候（也就是所谓的套圈），跑的快的那个人就比跑的慢的人整整多跑了一圈，所以环的长度也就出来了。

（3）如何确定环的起点
环的检测用上述原理，接下来我们来看一下如何确定环的起点，这也是Floyd解法的第二部分。方法是将其中一个指针移到链表起点，两者同时移动，每次移动一步，那么两者相遇的地方就是环的起点。

解析：
首先假设第一次相遇的时候慢指针走过的节点个数为i，设链表头部到环的起点的长度为m，环的长度为n，相遇的位置与起点与起点位置距离为k。
于是有：
i = m + a * n + k
其中a为慢指针走的圈数。

因为快指针的速度是慢指针的2倍，于是又可以得到另一个式子：
2 * i = m + b * n + k
其中b为快指针走的圈数。

两式相减得：
i = ( b - a ) * n
也就是说i是圈长的整数倍。

这是将其中一个节点放在起点，然后同时向前走m步时，此时从头部走的指针在m位置。而从相遇位置开始走的指针应该在距离起点i+m，i为圈长整数倍，则该指针也应该在距离起点为m的位置，即环的起点。

