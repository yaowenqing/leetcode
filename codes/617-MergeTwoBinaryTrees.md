合并两个二叉树。

![](https://github.com/yaowenqing/leetcode/blob/master/images/1.png)


### 代码

```
TreeNode* mergeTrees(TreeNode* t1, TreeNode* t2) {
        if(!t1) return t2;
        if(!t2) return t1;
        TreeNode*node=new TreeNode(t1->val+t2->val);
        node->left=mergeTrees(t1->left,t2->left);
        node->right=mergeTrees(t1->right,t2->right);
        return node;
    }
```
