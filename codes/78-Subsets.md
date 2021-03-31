Given a set of distinct integers, nums, return all possible subsets (the power set).

Note: The solution set must not contain duplicate subsets.

**Example**

Input: nums = [1,2,3]

Output:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]

***二进制解法***

To give all the possible subsets, we just need to exhaust all the possible combinations of the numbers. And each number has only two possibilities: either in or not in a subset. And this can be represented using a bit.

Using [1, 2, 3] as an example, 1 appears once in every two consecutive subsets, 2 appears twice in every four consecutive subsets, and 3 appears four times in every eight subsets (initially all subsets are empty):

[], [ ], [ ], [    ], [ ], [    ], [    ], [       ]

[], [1], [ ], [1   ], [ ], [1   ], [    ], [1      ]

[], [1], [2], [1, 2], [ ], [1   ], [2   ], [1, 2   ]

[], [1], [2], [1, 2], [3], [1, 3], [2, 3], [1, 2, 3]

```C++
 vector<vector<int>> subsets(vector<int>& nums) {
        int n=nums.size(),p=1<<n;
        vector<vector<int>> res(p);
        for(int i=0;i<p;i++){
            for(int j=0;j<n;j++){
                if((i>>j)&1)
                    res[i].push_back(nums[j]);
            }        
        }
        return res;
    }
```

***迭代解法***

以 [1, 2, 3]为例

Adding 1 to []: 

[[], [1]]; 

Adding 2 to [] and [1]:

 [[], [1], [2], [1, 2]]; 

Adding 3 to [], [1], [2] and [1, 2]: 

[[], [1], [2], [1, 2], [3], [1, 3], [2, 3], [1, 2, 3]].

```C++
 vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> res={{}};
        for(int num:nums){
            int n=res.size();
            for(int i=0;i<n;i++){
                res.push_back(res[i]);
                res[i].push_back(num);
            }       
        }
       return res; 
    }
```

JAVA
```java
public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res =new ArrayList<>();
        res.add(new ArrayList<>());
        for(int num:nums){
            int size=res.size();
            for(int i=0;i<size;i++){
                List<Integer> subres=new ArrayList<>(res.get(i));
                subres.add(num);
                res.add(subres);
            }
        }
        return res;
    }
```
