Given a binary tree, find its maximum depth. 

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node. 

### 代码

```
int maxDepth(TreeNode* root) {
    return root==NULL?0:max(maxDepth(root->left),maxDepth(root->right))+1;
}
```
