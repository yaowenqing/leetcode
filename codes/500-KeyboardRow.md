![](https://github.com/yaowenqing/leetcode/blob/master/images/6.png)

返回所给数组元素中，所有的字母都在键盘同一行的元素。 

### 解题思路

每一个单词在处理的时候，先压入，然后获取其第一个字母所在的键盘行数，再判断其他字母所在键盘行数，如果不为第一个字母所在的键盘行数就弹出该单词。

```
vector<string> findWords(vector<string>& words) {
    unordered_set<char> row1 {'q', 'w', 'e', 'r', 't', 'y','u', 'i', 'o', 'p'};
    unordered_set<char> row2 {'a', 's', 'd', 'f', 'g', 'h', 'j', 'k', 'l'}; 
    unordered_set<char> row3 { 'z', 'x', 'c', 'v', 'b' ,'n', 'm'};
    vector<unordered_set<char>> rows{row1,row2,row3};

    vector<string> validWords;

    for(int i=0;i<words.size();i++){
        validWords.push_back(words[i]);
        int row=0;
        for(int j=0;j<3;j++){
            if(rows[j].count((char)tolower(words[i][0]))>0)
                row=j; //获取第一个字母所在的键盘行数
        }
        for(int k=1;k<words[i].size();k++){
            //判断其他字母所在键盘行数，如果不为第一个字母所在的键盘行数，就弹出该单词
            if(rows[row].count((char)tolower(words[i][k]))==0){
                validWords.pop_back(); 
                break;
            }
        }
    }
    return validWords;
}
```
