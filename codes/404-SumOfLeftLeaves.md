求二叉树左叶子节点的值之和。 

![](https://github.com/yaowenqing/leetcode/blob/master/images/2.png)

### 代码

```
int sumOfLeftLeaves(TreeNode* root) {
    if (!root) return 0;
    if (root->left && !root->left->left && !root->left->right) 
        return root->left->val + sumOfLeftLeaves(root->right);
    return sumOfLeftLeaves(root->left) + sumOfLeftLeaves(root->right);
}

```
