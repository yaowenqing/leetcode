使用队列来存储树节点，教科书般的标准写法

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res=new ArrayList<>();
        if(root==null)
            return res;
        Queue<TreeNode> q=new LinkedList<>();
        q.add(root);
        while(!q.isEmpty()){
            List<Integer> subres=new ArrayList<>();
            int count=q.size();     
            while(count>0){
                TreeNode node=q.poll();
                subres.add(node.val);
                if(node.left!=null)
                    q.add(node.left);
                if(node.right!=null)
                    q.add(node.right);
                count--;
            }
            res.add(subres);
        }
        return res;    
    }
}
```
