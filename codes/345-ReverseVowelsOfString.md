Write a function that takes a string as input and reverse only the vowels of a string.

**Example 1**

Input: "hello"

Output: "holle"

**Example 2**

Input: "leetcode"

Output: "leotcede"

> Note:The vowels does not include the letter "y".

自己的方法：

```
string reverseVowels(string s) {
        int low=0,high=s.size();
        while(low<high){
            while(low<high&&!vowel(s[low])){
                low++;
            }               
            while(low<high&&!vowel(s[high])){
                 high--;
            }
            swap(s[high],s[low]);      
            low++;high--;       
        }
        return s;
    }
    
    bool vowel(char l){
        if(l == 'a'||l == 'e'||l == 'i'||l == 'o'||l == 'u'||l =='A'||l =='E'||l =='I'||l =='O'||l =='U')
           return true;
        else
           return false;
}
```

网上看到的方法：

```
string reverseVowels(string s) {
        int i = 0, j = s.size() - 1;
        while (i < j) {
            i = s.find_first_of("aeiouAEIOU", i);
            j = s.find_last_of("aeiouAEIOU", j);
            if (i < j) {
                swap(s[i++], s[j--]);
            }
        }
        return s;
    }
```
