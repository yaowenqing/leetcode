**迭代的方法：**

迭代的方法处理二叉树的后序遍历是最难的。

**方法1：**
用迭代的方法处理二叉树的前序遍历的时候，我们每次先把右子树的节点压栈，然后再把左子树的节点压栈，因此左子树会先出栈，保证了顺序是“中-左-右”

类似地，在后序遍历中，如果我们以“中-右-左”的顺序遍历二叉树，将结果压进栈中，弹栈的时候顺序就是“左->右->中”，也就是后序遍历的结果了。我们可以构造两个栈来解决这一问题。

步骤：
- 用stack1协助以“中->右->左”的顺序遍历二叉树，将结果保存到stack2中
- 依次弹出stack2中的元素即为二叉树的后序遍历结果

代码：
```java
class Solution { 
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res=new ArrayList<>();
        if(root==null)
            return res;
        Stack<TreeNode> sk1=new Stack<>();
        Stack<TreeNode> sk2=new Stack<>();
        sk1.push(root);
 
        while(!sk1.isEmpty()){         
            TreeNode node=sk1.pop();
            sk2.push(node);
            if(node.left!=null)
                sk1.push(node.left); 
            if(node.right!=null)
                sk1.push(node.right);                                          
        }
        while(!sk2.isEmpty()){
            res.add(sk2.pop().val);
        }
        return res;
    } 
}
```

**方法2**
或者我们可以不需要构造辅助栈，而是每次在res中加入元素不是在末尾加入而是插在最头的位置上。

```java
class Solution { 
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res=new ArrayList<>();
        if(root==null)
            return res;
        Stack<TreeNode> sk=new Stack<>();
        sk.push(root);
        while(!sk.isEmpty()){         
            TreeNode node=sk.pop();
            if(node.left!=null)
                sk.push(node.left);
            if(node.right!=null)
                sk.push(node.right);                       
            res.add(0,Integer.valueOf(node.val));
        }
        return res;
    } 
}
```


**递归的方法：**

构造一个新的函数用于递归：

```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res=new ArrayList<>();
        postorder(root,res);
        return res;
    }
    public void postorder(TreeNode root,List<Integer> res){
        if(root==null){
            return;
        }
        postorder(root.left,res);
        postorder(root.right,res);
        res.add(root.val);      
    }
}
```
或者直接在原函数上递归：
```java
class Solution {
    List<Integer> res=new ArrayList<>();
    public List<Integer> postorderTraversal(TreeNode root) {
        if(root==null)
            return res;        
        if(root.left!=null)
            postorderTraversal(root.left);
        if(root.right!=null)
            postorderTraversal(root.right);
        res.add(root.val);
        return res;
    }   
}
```
