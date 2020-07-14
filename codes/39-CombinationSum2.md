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
                if(i>start&&candidates[i]==candidates[i-1])
                    continue;
                temp.add(candidates[i]);
                comb(candidates,target-candidates[i],temp,i+1);
                temp.remove(temp.size()-1);
            }
        }
        
    }
}
```
