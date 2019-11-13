Using stack  
This is like 0144preorderTraversal, but we have to store all the left children in the stack first (in comparision, for preorder you don't need to store them first), and repeat for every left child.  

Steps cited from a leetcode post:  

1. We push all the left children of root into the stack until there's no more nodes.  
2. Then we pop from the stack which we'd call curr.  
3. Add curr to result list  
4. Push all the left children of curr.right into the stack (i.e. do step 1 again for curr.right)


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
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if (root == null) return res;
        
        Stack<TreeNode> stk = new Stack<>();
        stk.push(root);
        TreeNode curr = root;
        
        while (curr.left != null) {
            curr = curr.left;
            stk.push(curr);
        }
        while (!stk.isEmpty()) {
            curr = stk.pop();
            res.add(curr.val);
            if (curr.right != null) {
                curr = curr.right;
                stk.push(curr);
                while (curr.left != null) {
                    curr = curr.left;
                    stk.push(curr);
                }
            }
        }
        return res;
    }
}
```