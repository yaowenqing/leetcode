从下往上的二叉树层次遍历，注意和102题的对比，只有一行代码不一样

```java
class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> res =new ArrayList<>();
        if(root==null)
            return res;
        Queue<TreeNode> q=new LinkedList<>();
        q.add(root);
        while(!q.isEmpty()){
            List<Integer> subres=new ArrayList<>();
            int count=q.size();
            while(count>0){
                TreeNode node = q.poll();
                subres.add(node.val);
                if(node.left!=null)
                    q.add(node.left);
                if(node.right!=null)
                    q.add(node.right);
                count--;
            }
            res.add(0,subres);
        }
        return res;
    }
}
```
