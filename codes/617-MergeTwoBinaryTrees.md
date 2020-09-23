合并两个二叉树。

![](https://github.com/yaowenqing/leetcode/blob/master/images/1.png)


### 代码

```C++
TreeNode* mergeTrees(TreeNode* t1, TreeNode* t2) {
        if(!t1) return t2;
        if(!t2) return t1;
        TreeNode*node=new TreeNode(t1->val+t2->val);
        node->left=mergeTrees(t1->left,t2->left);
        node->right=mergeTrees(t1->right,t2->right);
        return node;
    }
```
JAVA:

```java
class Solution {
    public TreeNode mergeTrees(TreeNode t1, TreeNode t2) {
        TreeNode res=new TreeNode();
        if(t1==null){
            return t2;
        }
        if(t2==null){
            return t1;
        }      
        res.val=t1.val+t2.val;
        res.left=mergeTrees(t1.left,t2.left);
        res.right=mergeTrees(t1.right,t2.right);
        return res;
    }
}
```
