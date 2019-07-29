Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center). 

![](https://github.com/yaowenqing/leetcode/blob/master/images/5.jpg)

> Note:Bonus points if you could solve it both recursively and iteratively. 

### 代码

递归解法（DFS）：

```
bool isSymmetric(TreeNode* root) {
        if(root==NULL)
            return true;
        return isMirror(root->left,root->right);
}

bool isMirror(TreeNode* root1,TreeNode* root2){
        if(root1==NULL && root2==NULL)
            return true;
        if(root1==NULL || root2==NULL)
            return false;
        return (root1->val==root2->val && isMirror(root1->left,root2->right) && 
               isMirror(root1->right,root2->left));    

}
```

迭代解法（BFS）：


```
bool isSymmetric(TreeNode* root) {
        if(!root)
            return true;
        TreeNode*l = root->left;
        TreeNode*r = root->right;

        queue<TreeNode*>left;
        queue<TreeNode*>right;

        left.push(l);
        right.push(r);

        while(!left.empty()&&!right.empty()){      
            l=left.front();
            r=right.front();
            left.pop();
            right.pop();
            if(l==NULL&&r==NULL)
                continue;
            if(l==NULL||r==NULL)
                return false;
            if(l->val!=r->val)
                return false;
            left.push(l->left);
            left.push(l->right);
            right.push(r->right);
            right.push(r->left);
        }
        return true;
    }
```
