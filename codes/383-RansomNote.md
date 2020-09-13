Given an arbitrary ransom note string and another string containing letters from all the magazines, write a function that will return true if the ransom note can be constructed from the magazines ; otherwise, it will return false.

Each letter in the magazine string can only be used once in your ransom note.

>Example 1:
Input: ransomNote = "a", magazine = "b"
Output: false

>Example 2:
Input: ransomNote = "aa", magazine = "ab"
Output: false

>Example 3:
Input: ransomNote = "aa", magazine = "aab"
Output: true

最容易想到的，用哈希表存储来解决问题，可以通过。

```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        HashMap<Character,Integer> map=new HashMap<>();
        for(int i=0;i<magazine.length();i++){
            char c=magazine.charAt(i);
            if(map.containsKey(c))
                map.put(c,map.get(c)+1);                
            else
                map.put(c,1);          
        }
        for(int j=0;j<ransomNote.length();j++){
            char d=ransomNote.charAt(j);
            if(map.containsKey(d)&&map.get(d)>0)
                map.put(d,map.get(d)-1);
            else
                return false;
        }
        return true;
    }
}
```

看到了一个更节省时间的算法，只需要O(n)的复杂度。

构建一个index数组，用来存储每个字符在magazine中每次寻找出现的位置，如果位置是-1说明没找到；如果找到了，就把这个对应字符出现的位置+1记录在index数组里，用于下次可能的寻找。

```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        if(ransomNote==null)
            return true;
        if(magazine==null)
            return false;
        int index[]=new int[128];
        for(int i=0;i<ransomNote.length();i++){
            char c=ransomNote.charAt(i);
            int find=magazine.indexOf(c,index[c]);
            if(find==-1)
                return false;
            else
                index[c]=find+1;
        }
        return true;
    }
}
```
