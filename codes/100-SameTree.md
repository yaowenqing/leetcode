判断两个二叉树是否完全相同 

我最开始的解法：

```
bool isSameTree(TreeNode* p, TreeNode* q) {
    if(p==NULL&&q==NULL)
        return true;
    else if(p==NULL&&q!=NULL||q==NULL&&p!=NULL)
        return false;
    if(p->val!=q->val)
        return false;
    if(isSameTree(p->left,q->left)&&isSameTree(p->right,q->right))
        return true;
    else 
        return false;
}
```

显然有些复杂，下面是一个更优雅的解法：


```
bool isSameTree(TreeNode* p, TreeNode* q) {
    if(!p && !q)
        return true;
    else if (p && q)
        return (p->val == q->val && isSameTree(p->left, q->left) && isSameTree(p->right,q->right));
    else return false;
}
```

Java版本
```java
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if(p==null && q==null)
            return true;
        else if(p!=null && q!=null)
            return (p.val==q.val && isSameTree(p.left,q.left) && isSameTree(p.right,q.right));
        else 
            return false;
    }
}
```
