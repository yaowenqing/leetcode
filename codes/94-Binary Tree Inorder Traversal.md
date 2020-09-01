二叉树的中序遍历

```java
public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res=new ArrayList<>();
        inorder(root,res);
        return res;       
    }
    public void inorder(TreeNode T,List<Integer> l){
        if(T==null)
            return;
        inorder(T.left,l);
        l.add(T.val);
        inorder(T.right,l);
    }
```
