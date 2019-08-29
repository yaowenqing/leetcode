There are N children standing in a line. Each child is assigned a rating value.

You are giving candies to these children subjected to the following requirements:

- Each child must have at least one candy. 
- Children with a higher rating get more candies than their neighbors. 

What is the minimum candies you must give?

**Example 1**

Input: [1,0,2]

Output: 5

Explanation: You can allocate to the first, second and third child with 2, 1, 2 candies respectively.

**Example 2**

Input: [1,2,2]

Output: 4

Explanation: You can allocate to the first, second and third child with 1, 2, 1 candies respectively.

解题思路：先从左往右扫，遇到当前小孩rating值大于前一个小孩rating值，则给该小孩分的糖置为前一个小孩糖果数加一。

然后从右往左扫，遇到当前小孩rating值小于后面小孩的rating值，则后面小孩的糖果数为后面小孩临时分配的糖果数和当前小孩分配的糖果数加一两者之中的最大值。

```
int candy(vector<int>& ratings) {
        int n=ratings.size();
        int total=0;;
        vector<int> alloc(n,1);
        for(int i=1;i<n;i++){
            if(ratings[i]>ratings[i-1])
                alloc[i]=alloc[i-1]+1;            
        }
        int res=alloc[n-1];
        for(int j=n-2;j>=0;j--){
            if(ratings[j]>ratings[j+1])
                alloc[j]=max(alloc[j],alloc[j+1]+1);
            res+=alloc[j];
        }
        return res;
    }
```
