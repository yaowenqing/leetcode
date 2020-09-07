我的解法：引入了maxDepth来求二叉树深度，然后依次对比每个节点的左右孩子深度之差。

```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        if(root==null)
            return true;
        if(Math.abs(height(root.left)-height(root.right))>1)
            return false;
        else
            return isBalanced(root.left)&&isBalanced(root.right);       
    }
    public int height(TreeNode node){
        if(node==null)
            return 0;
        return 1+Math.max(height(node.left),height(node.right));
    } 
}
```

发现，在每次求height的时候有大量的重复运算，为了避免这种重复运算，我们考虑我们在遍历一遍树（求一次height）的过程中就可以得到答案，此时我们希望当左右子树中存在不平衡的时候就可以提前停止。

对于我的方法的改进，一个更巧妙的方法，当树不平衡时直接让高度为-1，避免了后续还要重复计算height的情况：

```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        return height(root)!=-1;
    }
    private int height(TreeNode node){
        if(node==null){
            return 0;
        }
        int left=height(node.left);
        int right=height(node.right);
        if(left==-1||right==-1||Math.abs(right-left)>1)
            return -1;
        else 
            return Math.max(left,right)+1;
    }
}
```
