# LC590. N-ary Tree Postorder Traversal

### LeetCode

## Question

Given an n-ary tree, return the postorder traversal of its nodes' values.
 
For example, given a 3-ary tree:

![LC590. N-ary Tree Postorder Traversal](images/LC590N-aryTreePostorderTraversal.png)

Return its postorder traversal as: [5,6,3,2,4,1].
 
**Note:** Recursive solution is trivial, could you do it iteratively?

## Solutions

* Java1
```
class Solution {
    public List<Integer> postorder(Node root) {
        List<Integer> res = new LinkedList();
        helper(root, res);
        return res;
    }
    
    private void helper(Node root, List<Integer> res){
        if(root == null) return;
        for(Node node : root.children)
            helper(node, res);
        res.add(root.val);
    }
}
```

# Explanation

It's similar with binary tree.

* **worst-case time complexity:** O(log(n)), where n is the number of the nodes in the tree.
* **worst-case space complexity:** O(log(n)), where n is the number of the nodes in the tree.
