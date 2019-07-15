Given a 32-bit signed integer, reverse digits of an integer. 

- Example 1:  

Input: 123  Output: 321 

- Example 2:  

Input: -123  Output: -321 

- Example 3:  

Input: 120  Output: 21 

> Note:Assume we are dealing with an environment which could only hold integers within the 32-bit signed integer range. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.  

```
int reverse(int x) {
        int i=x,bit=0;
        long long result=0;
        vector<int>number;
        while(i!=0){
            number.push_back(i%10);
            i=i/10;
            bit++;
        }
        for(int i=0;i<number.size();i++){
            result+=number[i]*pow(10,bit-1);
            bit--;
        }
        return (result<INT_MIN || result>INT_MAX) ? 0 : result;
    }

```
