# Lint376. Binary Tree Path Sum

### LintCode

## Question

Given a binary tree, find all paths that sum of the nodes in the path equals to a given number target.

A valid path is from root node to any of the leaf nodes.

**Example 1:**
```
Input:
{1,2,4,2,3}
5

Output: 
[[1, 2, 2],[1, 4]]

Explanation:
The tree is look like this:
	     1
	    / \
	   2   4
	  / \
	 2   3
For sum = 5 , it is obviously 1 + 2 + 2 = 1 + 4 = 5
```

**Example 2:**
```
Input:
{1,2,4,2,3}
3

Output: 
[]

Explanation:
The tree is look like this:
	     1
	    / \
	   2   4
	  / \
	 2   3
Notice we need to find all paths from root node to leaf nodes.
1 + 2 + 2 = 5, 1 + 2 + 3 = 6, 1 + 4 = 5 
There is no one satisfying it.
```

## Solutions

### Solution 1

* Java
```
public class Solution {
    /*
     * @param root: the root of binary tree
     * @param target: An integer
     * @return: all valid paths
     */
    public List<List<Integer>> binaryTreePathSum(TreeNode root, int target) {
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> group = new ArrayList<>();
        checkPathSum(root, target, res, group);
        return res;
    }
    
    private void checkPathSum(TreeNode root, int target, List<List<Integer>> res, List<Integer> group){
        if (root == null) return;
        if (root.left == null && root.right == null) {
            if (target == root.val) {
                group.add(root.val);
                res.add(group);
            }
            return;
        }
        group.add(root.val);
        List<Integer> right = new ArrayList<>();
        for (Integer g : group)
            right.add(g);
        checkPathSum(root.left, target-root.val, res, group);
        checkPathSum(root.right, target-root.val, res, right);
    }
}
```

The idea is very obviously, recursive a binary tree. But there are two trick points:

1. Compare the sum and the target only when you reach the leaf node.
2. You cannot use the same `group` in both child trees.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the number of nodes in the tree `root`.
* **worst-case space complexity:** `O(n)`, where `n` is the number of nodes in the tree `root`.
