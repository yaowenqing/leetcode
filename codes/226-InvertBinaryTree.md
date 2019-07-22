递归的思想，对根节点的左右子树调用该翻转函数，然后交换左右子树。

代码如下：

```
TreeNode* invertTree(TreeNode* root) {
        if(!root)
            return NULL;
        TreeNode* left=invertTree(root->left);
        TreeNode* right=invertTree(root->right);
        root->left=right;
        root->right=left;
        return root;
    }
```
