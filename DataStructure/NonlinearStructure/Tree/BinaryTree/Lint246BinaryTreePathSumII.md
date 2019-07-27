# Lint246. Binary Tree Path Sum II

### LintCode

## Question

Your are given a binary tree in which each node contains a value. Design an algorithm to get all paths which sum to a given value. The path does not need to start or end at the root or a leaf, but it must go in a straight line down.

**Example 1:**

```
Input:
{1,2,3,4,#,2}
6

Output:
[[2, 4],[1, 3, 2]]

Explanation:
The binary tree is like this:
    1
   / \
  2   3
 /   /
4   2
for target 6, it is obvious 2 + 4 = 6 and 1 + 3 + 2 = 6.
```

**Example 2:**

```
Input:
{1,2,3,4}
10

Output:
[]

Explanation:
The binary tree is like this:
    1
   / \
  2   3
 /   
4   
for target 10, there is no way to reach it.
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
    public List<List<Integer>> binaryTreePathSum2(TreeNode root, int target) {
        // write your code here
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> row = new ArrayList<>();
        if (root == null) return res; // exit of the current recursion
        
        binaryTreeSub(root, target, res, row, 0);
        res.addAll(binaryTreePathSum2(root.left, target)); // must after the binaryTreeSub
        res.addAll(binaryTreePathSum2(root.right, target));
        
        return res;
    }
    
    private void binaryTreeSub(TreeNode root, int target, List<List<Integer>> res, List<Integer> row, int sum) {
        if (root == null) {
            return;
        }
        
        row.add(root.val);
        
        if (sum + root.val == target) {
            res.add(new ArrayList<>(row));
        }
        
        // must without condition, in case of negative values
        List<Integer> right = new ArrayList<>(row);
        binaryTreeSub(root.left, target, res, row, sum + root.val);
        binaryTreeSub(root.right, target, res, right, sum + root.val);
       
    }
}
```

`The path does not need to start or end at the root or a leaf` is the challenge part of this question. The solution is to run the `binaryTreePathSum2` at every TreeNode in the tree.

**NOTE:**

1. Exit points of the two recursions.
2. The order of the two recursions.
3. There might be negative values in the tree.
4. Need new List when adding result, recursiving to left and right.

**Complexity:**

* **worst-case time complexity:** O(n<sup>log(n)</sup>), where `n` is the number of nodes of the tree `root`.
* **worst-case space complexity:** `O(n)`, where `n` is the number of nodes of the tree `root`.
