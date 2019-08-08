Given an array of strings, group anagrams together.

**Example**

Input: ["eat", "tea", "tan", "ate", "nat", "bat"],

Output:

[

  ["ate","eat","tea"],
  
  ["nat","tan"],
  
  ["bat"]
  
]

Note:
- All inputs will be in lowercase. 
- The order of your output does not matter.

代码：

```
vector<vector<string>> groupAnagrams(vector<string>& strs) {
        vector<vector<string>> res;
        unordered_map<string,vector<string>>map;
        
        for(auto s:strs){
            string temp=s;
            sort(temp.begin(),temp.end());
            map[temp].push_back(s);
        }
        
        for(auto it=map.begin();it!=map.end();it++){
            res.push_back(it->second);
        }
        return res;
}
```
