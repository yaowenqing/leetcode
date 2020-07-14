Given a collection of candidate numbers (candidates) and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target.

Each number in candidates may only be used once in the combination.

Note:

- All numbers (including target) will be positive integers.
- The solution set must not contain duplicate combinations.

> Example 1:
Input: candidates = [10,1,2,7,6,1,5], target = 8,
A solution set is:
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]

>Example 2:
Input: candidates = [2,5,2,1,2], target = 5,
A solution set is:
[
  [1,2,2],
  [5]
]

**思路**

这道题和39题之间的关系就好比47题和46题的关系，这四道题可以组合起来看。

类似47题，在处理有重复元素的情况时要先对数组排序。

这道题的处理相对简单，只需要在每次循环中加入元素是否重复的判断即可，若重复就跳过。

另外还要注意和39题的一个不同之处在于在函数中递归调用时的最后一个参数为i+1,这是因为此时我们不需要再考虑i这个位置的元素了（因为元素不能被重复使用）

>comb(candidates,target-candidates[i],temp,i+1);

**代码**

```java
class Solution {
    
    List<List<Integer>>res =new ArrayList<>();
    
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<Integer> temp=new ArrayList<>();
        Arrays.sort(candidates);
        comb(candidates,target,temp,0);
        return res;        
    }
    
    public void comb(int[] candidates,int target,List<Integer> temp,int start){
        if(target<0)
            return;
        else if(target==0)
            res.add(new ArrayList<>(temp));
        else{
            for(int i=start;i<candidates.length;i++){
                if(i>start&&candidates[i]==candidates[i-1])//直接跳过重复元素
                    continue;
                temp.add(candidates[i]);
                comb(candidates,target-candidates[i],temp,i+1);
                temp.remove(temp.size()-1);
            }
        }
        
    }
}
```
