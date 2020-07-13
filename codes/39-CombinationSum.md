Given a set of candidate numbers (candidates) (without duplicates) and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target.

The same repeated number may be chosen from candidates unlimited number of times.

Note:

- All numbers (including target) will be positive integers.
- The solution set must not contain duplicate combinations.

>Example 1:
Input: candidates = [2,3,6,7], target = 7,
A solution set is:
[
  [7],
  [2,2,3]
]

>Example 2:
Input: candidates = [2,3,5], target = 8,
A solution set is:
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]

和46、47题有一点类似。采用递归回溯的思想，每一次把candidates的第一个数字X加入temp，然后再次调用算法，target替换为target-X，调用结束后去掉temp顶端的数字。

举例，对于candidates = [2,3,5], target = 8。首先加入2，然后对candidates = [2,3,5], target = 6调用算法，此时的标记位i依然在2的位置。

最后，加入剪枝的策略，如果已经放入temp的数字加在一起超过了target，那么直接返回并去掉temp顶端的数字。

再举例，对于candidates = [2,3,6,7], target = 7。首先加入2。然后对candidates = [2,3,5], target =5调用算法，再加入2，再加入2，再加入2，此时对candidates = [2,3,5], target = -1调用算法（标记位i依然在2的位置），发现target<0，直接返回并去掉顶端的2。此时相当于对candidates = [2,3,5], target = 1走完了第一次循环，标记位移动到3，依然不能满足，标记位移动到6和7还是不能满足，此时走完所有循环，之后返回，再去掉顶端的2。相当于对candidates = [2,3,5], target = 3走完了第一次循环，标记位移动到3，满足，返回一组成功的结果。以此类推。

```java
    List<List<Integer>> res=new ArrayList<>();
    
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<Integer> temp=new ArrayList<>();
        comb(candidates,target,temp,0);
        return res;
    }
    
    public void comb(int[] candidates,int target,List<Integer> temp,int start){
        if(target<0) //剪枝
            return;
        else if(target==0)
            res.add(new ArrayList<>(temp));
        else{
            for(int i=start;i<candidates.length;i++){
                temp.add(candidates[i]);
                comb(candidates,target-candidates[i],temp,i);
                temp.remove(temp.size()-1);
            }
        }
    }
```
