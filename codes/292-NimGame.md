### 题目



You are playing the following Nim Game with your friend: There is a heap of stones on the table, each time one of you take turns to remove 1 to 3 stones. The one who removes the last stone will be the winner. You will take the first turn to remove the stones.  

Both of you are very clever and have optimal strategies for the game. Write a function to determine whether you can win the game given the number of stones in the heap.  

For example, if there are 4 stones in the heap, then you will never win the game: no matter 1, 2, or 3 stones you remove, the last stone will always be removed by your friend.  



### 思路



只要起手的石子数量不是4的倍数，先拿的人就必胜。 

先拿的人只需要拿1或2或3颗石子使剩下的石子数目为4的倍数即可。



### 代码



```

bool canWinNim(int n) {
    return (n%4!=0);
}

```
