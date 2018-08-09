# LC589. N-ary Tree Preorder Traversal

### LeetCode

## Question

Given an n-ary tree, return the preorder traversal of its nodes' values.
 
For example, given a 3-ary tree:

![LC589. N-ary Tree Preorder Traversal](Images/LC589N-aryTreePreorderTraversal.png)
 
Return its preorder traversal as: [1,3,5,6,2,4].
 
**Note:** Recursive solution is trivial, could you do it iteratively?

## Solutions
* Java1
```
class Solution {
    public List<Integer> preorder(Node root) {
        List<Integer> res = new LinkedList();
        preorder(root, res);
        return res;
    }
    
    private void preorder(Node root, List<Integer> res){
        if(root == null) return;
        res.add(root.val);
        for(Node n : root.children)
            preorder(n, res);
    }
}
```

# Explanation

It's similar with binary tree.

* **worst-case time complexity:** O(log(n)), where n is the number of the nodes in the tree.
* **worst-case space complexity:** O(log(n)), where n is the number of the nodes in the tree.
