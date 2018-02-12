# LC783. Minimum Distance Between BST Nodes

### LeetCode

Given a Binary Search Tree (BST) with the root node root, return the minimum difference between the values of any two different nodes in the tree.

**Example :**
```
Input: root = [4,2,6,1,3,null,null]
Output: 1
```

**Explanation:**

Note that root is a TreeNode object, not an array.

The given tree `[4,2,6,1,3,null,null]` is represented by the following diagram:

```
          4
        /   \
      2      6
     / \    
    1   3  
```

while the minimum difference in this tree is 1, it occurs between node 1 and node 2, also between node 3 and node 2.

**Note:**

* The size of the BST will be between 2 and 100.
* The BST is always valid, each node's value is an integer, and each node's value is different.

## Solutions

* Java1
```
class Solution {
    public int minDiffInBST(TreeNode root) {
        int res = Integer.MAX_VALUE;
        if(root.left==null && root.right==null)
            return res;
        if(root.left != null)
            res = Math.min(Math.abs(root.val - maxBST(root.left)), minDiffInBST(root.left));
        if(root.right != null)
            res = Math.min(res, Math.min(Math.abs(root.val - minBST(root.right)), minDiffInBST(root.right)));
        return res;
    }
    
    private int maxBST(TreeNode root){
        while(root.right != null) root = root.right;
        return root.val;
    }
    
    private int minBST(TreeNode root){
        while(root.left != null) root = root.left;
        return root.val;
    }
}
```

## Explanation

For each node, the minimum difference is between the node's value and the left children's maximum value or the right children's minimum value.

Then recurse every node in the tree.

* **worst-case time complexity:** O((log(n))<sup>2</sup>)
* **worst-case space complexity:** O(1)