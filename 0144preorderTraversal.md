Using stack   
The idea is to use a stack to store in some order (depending on {pre,in,post}+order traversal). The difference only lies in how the nodes are stored.  

for preorder (root->left->right), in the iteration:  

* first put current value in result list
* push the right child(if exists) into stack, because we want to search it at last.
* push the left child into stack, we want to search it first.  


```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if (root == null) return res;
        //init set-up
        Stack<TreeNode> stk = new Stack<>();
        stk.push(root);
        //start traversing
        while (!stk.isEmpty()) {
            TreeNode curr = stk.pop();
            res.add(curr.val);
            if (curr.right != null) stk.push(curr.right);
            if (curr.left != null) stk.push(curr.left);
        }
        
        return res;
        
    }
}
```
