![](https://github.com/yaowenqing/leetcode/blob/master/images/7.png)

### 思路

通过观察发现，从最高的点（塔顶）往两边遍历，水位只会减小不会升高。

从两边往中间遍历，水位一直和最近遇到的最大高度持平。这样知道了实时水位，就可以边遍历边计算面积。

### 代码

```
int trap(vector<int>& height) {
        int n=height.size();
        if(n<=2)
            return 0;
        int max=-1,maxPos=-1;
        for(int i=0;i<n;i++){
            if(height[i]>max){
                max=height[i];
                maxPos=i;
            }
        }
        int area=0,root=height[0];
        for(int i=1;i<maxPos;i++){
            if(root<height[i])
                root=height[i];
            else
                area+=(root-height[i]);
        }
        root=height[n-1];
        for(int j=n-2;j>maxPos;j--){
            if(root<height[j])
                root=height[j];
            else
                area+=(root-height[j]);        
        }
        return area;
    }
```
