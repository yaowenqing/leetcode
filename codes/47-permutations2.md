Given a collection of numbers that might contain duplicates, return all possible unique permutations.

思路：类似 46题，都是逐一将元素添加到中间集中，然后将中间集添加到结果集中。由于数据有重复，如果不加以处理的话，[1,1,2]这样的实例就会出现重复的结果。为了避免出现重复的情况，对与重复的元素循环时，跳过递归的调用，只对第一个未被使用的进行递归，保证每次的结果将会唯一出现在结果集中，而后重复的元素将会被略过。如果第一个重复元素还没在当前结果中，那么我们就不需要进行递归。

另外需要说明的是在进行处理之前需要对数组进行排序，保证相同的元素挨在一起。

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
