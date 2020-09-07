
Given a binary tree, find its minimum depth.

- The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.


Example:

>Given binary tree [3,9,20,null,null,15,7]
return its minimum depth = 2.

注意和最大深度的不同，要考虑到左子树和右子树有一个为空的情况，我写的代码如下：

```java
class Solution {
    public int minDepth(TreeNode root) {
        if(root==null)
            return 0;
        if(root.left==null&&root.right==null)
            return 1;
        if(root.left==null)
            return 1+minDepth(root.right);
        if(root.right==null)
            return 1+minDepth(root.left);
        return 1+Math.min(minDepth(root.left),minDepth(root.right));     
    }
}
```

看到别的的另一种写法（其实本质上都差不多）
```java
class Solution {
    public int minDepth(TreeNode root) {
        if (root == null)return 0;
        if (root.left == null || root.right == null) {
            return Math.max(minDepth(root.left),minDepth(root.right))+1;
        }
        return Math.min(minDepth(root.left),minDepth(root.right))+1;
    }
}
```
