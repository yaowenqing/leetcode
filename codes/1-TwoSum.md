Given an array of integers, return indices of the two numbers such that they add up to a specific target. 

You may assume that each input would have exactly one solution, and you may not use the same element twice. 

**Example**


Given nums = [2, 7, 11, 15], target = 9 

Because nums[0] + nums[1] = 2 + 7 = 9, 

return [0, 1].

最开始的代码

```
vector<int> twoSum(vector<int>& nums, int target) {
        vector<int>res;
        for(int i=0;i<nums.size()-1;i++){
            for(int j=i+1;j<nums.size();j++){
                if(nums[i]+nums[j]==target){
                    res.push_back(i);
                    res.push_back(j);
                }
            }
        }
        return res;
    }
```

虽然通过了，但是时间为250ms，太慢了。 

下面是时间复杂度为n的解决方案。

```
vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> hash;
        vector<int> result;
        for (int i = 0; i < nums.size(); i++) {
            int numberToFind = target - nums[i];
            if (hash.find(numberToFind) != hash.end()) {
                result.push_back(hash[numberToFind]);
                result.push_back(i);            
                return result;
            }          
        hash[nums[i]] = i;
    }
    return result;      
}
```
