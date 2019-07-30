There are N gas stations along a circular route, where the amount of gas at station i is gas[i].

You have a car with an unlimited gas tank and it costs cost[i] of gas to travel from station i to its next station (i+1). You begin the journey with an empty tank at one of the gas stations.

Return the starting gas station’s index if you can travel around the circuit once in the clockwise direction, otherwise return -1.

Note:

- If there exists a solution, it is guaranteed to be unique.
- Both input arrays are non-empty and have the same length.
- Each element in the input arrays is a non-negative integer.


**Example 1**


Input:  

  gas  = [1,2,3,4,5] 

cost = [3,4,5,1,2] 

Output: 3 

Explanation: 

```
  Start at station 3 (index 3) and fill up with 4 unit of gas. Your tank = 0 + 4 = 4 
  Travel to station 4. Your tank = 4 - 1 + 5 = 8 
  Travel to station 0. Your tank = 8 - 2 + 1 = 7 
  Travel to station 1. Your tank = 7 - 3 + 2 = 6 
  Travel to station 2. Your tank = 6 - 4 + 3 = 5 
  Travel to station 3. The cost is 5. Your gas is just enough to travel back to station 3. 
  Therefore, return 3 as the starting index.
```

**Example 2**


Input:  

gas  = [2,3,4] 

cost = [3,4,3] 

Output: -1 

Explanation: 

```
  You can’t start at station 0 or 1, as there is not enough gas to travel to the next station. 
  Let’s start at station 2 and fill up with 4 unit of gas. Your tank = 0 + 4 = 4 
  Travel to station 0. Your tank = 4 - 3 + 2 = 3 
  Travel to station 1. Your tank = 3 - 3 + 3 = 3 
  You cannot travel back to station 2, as it requires 4 unit of gas but you only have 3. 
  Therefore, you can’t travel around the circuit once no matter where you start.
```

初始解法：暴力二重循环

```
int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        int n=gas.size();
        vector<int> cur(n);
        int res;
        for(int i=0;i<n;i++){
            int signal=0;
            cur[i]=gas[i];
            for(int j=i;j<i+n;j++){
                int real=j%n;
                int nextReal=(j+1)%n;
                cur[real]=cur[real]-cost[real];
                if(cur[real]<0)
                    break; 
                cur[nextReal]=cur[real]+gas[nextReal];
                signal++;
            }
            if(signal==n)
                return i;
        }
        return -1;
}
```

虽然AC了，但是太慢了，用了151ms

下面介绍一个巧妙的方法，用时直接变为7ms：

思路：remain的含义是当前剩下的所有燃料，如果现在剩下的所有燃料不够开到下一个地方（即remain<0）,那么这不是一个成功的起始位置，执行三个步骤：

- 把remain加入debt里面，代表欠下的燃料。
- 剩余的所有燃料归零，这是为了不影响后续的计算，同时既然把remain的值加在了debt之中，这次迭代中remain的值也就失去了意义。
- （最难理解的一步，一会儿详细讲）把start所指的位置挪动到当前遍历位置的下一个位置，而不是对start进行++的操作。

遍历n个位置之后，比较remain和debt的绝对值大小来决定是否可以成功地完成一个环路。

讲解刚才的第三步： 

疑惑：如果我们从start=0的地方开始，遍历第0个、第1个、第2个位置时remain都大于0，但是在第3个位置remain小于0了，这证明从第0个地方开始是行不通的，我们需要改变start的大小。这个时候按照我们的算法，start应该被赋值为4，那为什么不是1或者是2呢？

引入一个定理：


> 定理1：If  the car starts at A and can not reach B.(B is the first station that A can not reach.)，then any station between A and B can not reach B.


**定理1的证明**：按照定理的条件，A可以到达B之前的任意一个点，那么当A到达X（X代表A和B之间任意一个点）时假设车上的汽油为g（g>=0）。那么如果从X开始带着量为g的汽油不能到达B。那么如果X是起点，带着量为0的汽油更不可能到达B。

按照这个定理，对于刚才的情况，我们没有必要再对1、2、3进行尝试，直接把start设置为4即可。

这个时候还有一个问题没有解决，观察return语句，在我们已知remain+debt>=0，也即总油量不小于总消耗的情况下，我们如何确定从start这个点开始一定可以符合我们的要求呢？引入定理2：


> 定理2：If the total number of gas is bigger than the total number of cost. There must be a solution.

或者用更一般化的语言：（这里的数组元素为gas-cost）

> 定理2：如果一个数组的总和非负，那么一定可以找到一个起始位置，从他开始绕数组一圈，累加和一直都是非负的

既然定理2成立，那么一定存在一个解决方案，start这个点也就一定是我们所要的答案。

代码如下：

```
 int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        int start=0; // 起始位置
        int remain=0; //当前剩余燃料
        int debt=0; //所有当前燃料不够的情况下所欠的总债
        for(int i=0;i<gas.size();i++){
            remain+=gas[i]-cost[i];
            if(remain<0){ //燃料要欠债
                debt+=remain;
                start=i+1; //说明这绝对不是一个可以成功的起始位置，起始位置向下移动
                remain=0; //剩余燃料清空
            }
        }
        return remain+debt>=0?start:-1;
    }
```
