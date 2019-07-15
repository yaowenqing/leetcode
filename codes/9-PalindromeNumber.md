Determine whether an integer is a palindrome. Do this without extra space. 

### 代码

```
bool isPalindrome(int x) {
        long long orginal=x;
        if(orginal<0)
            return false;
        long long reverse=0;
        while(x){
            reverse=reverse*10+x%10;
            x=x/10;
        }
        if(reverse==orginal)
            return true;
        else
            return false;
    }
```
