### 题目

爬台阶，爬n阶，每次1阶或2阶，求所有可能方案的数目。

### 思路

最简易的动态规划模型

### 代码

```
int climbStairs(int n) {
        vector<int> steps(n);
        steps[0]=1;
        steps[1]=2;
        for(int i=2;i<n;i++){
            steps[i]=steps[i-2]+steps[i-1];
        }
        return steps[n-1];
    }
```

