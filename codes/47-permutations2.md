Given a collection of numbers that might contain duplicates, return all possible unique permutations.

>Example:
Input: [1,1,2]
Output:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]

```java
    List<List<Integer>> res = new ArrayList<List<Integer>>();
    boolean[] used=null;
    public List<List<Integer>> permuteUnique(int[] nums) {
        used=new boolean[nums.length];
        Arrays.sort(nums);
        perm(nums,0,new ArrayList<>());
        return res;
    }
    
    public void perm(int[] nums,int index,List<Integer> st){
        if(index==nums.length){
            List<Integer> list =new ArrayList<>(st);
            res.add(list);
        }else{
            for(int i=0;i<nums.length;i++){
                if(used[i])
                    continue;
                if(i>0 && nums[i-1]==nums[i] && !used[i-1])
                    continue;
                
                st.add(nums[i]);
                used[i]=true;
                perm(nums,index+1,st);
                used[i]=false;
                st.remove(st.size()-1);
            }
        }
    }
```
