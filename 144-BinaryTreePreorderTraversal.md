
二叉树前序遍历

迭代的方法：
```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> res=new ArrayList<>();
        if(root==null)
            return res;
        Stack<TreeNode> sk=new Stack<>();
        sk.push(root);
        while(!sk.isEmpty()){
            TreeNode node=sk.pop();
            res.add(Integer.valueOf(node.val));
            if(node.right!=null)
                sk.push(node.right);
            if(node.left!=null)
                sk.push(node.left);
        }        
        return res;
    }
}
```

递归的方法：
```java
class Solution {
     List<Integer> res=new ArrayList<>();
     public List<Integer> preorderTraversal(TreeNode root) {              
         if(root==null)
             return res;
         res.add(root.val);
         if(root.left!=null)
             preorderTraversal(root.left);
         if(root.right!=null)   
             preorderTraversal(root.right);
         return res;
    }
}
```
