求二叉树左叶子节点的值之和。 

![](https://github.com/yaowenqing/leetcode/blob/master/images/2.png)

### 代码

递归，C++版本：

```C++
int sumOfLeftLeaves(TreeNode* root) {
    if (!root) return 0;
    if (root->left && !root->left->left && !root->left->right) 
        return root->left->val + sumOfLeftLeaves(root->right);
    return sumOfLeftLeaves(root->left) + sumOfLeftLeaves(root->right);
}

```

java版本：

```java
class Solution {
    public int sumOfLeftLeaves(TreeNode root) {
        if(root==null)
            return 0;
        if(root.left!=null && root.left.left==null && root.left.right==null)
            return root.left.val+sumOfLeftLeaves(root.right);
        return sumOfLeftLeaves(root.left)+sumOfLeftLeaves(root.right);
    }
}
```
