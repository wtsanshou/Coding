# Lint164. Unique Binary Search Trees II

### LintCode

## Question

Given n, generate all structurally unique BST's (binary search trees) that store values 1...n.

**Example 1:**

```
Input:
3

Output:
    1         3     3       2    1
     \       /     /       / \    \
      3     2     1       1   3    2
     /     /       \                \
    2     1         2                3
```

## Solutions

### Solution 1

* Java

```
public class Solution {
    /**
     * @paramn n: An integer
     * @return: A list of root
     */
    public List<TreeNode> generateTrees(int n) {
        return generateBSTfrom(1, n);
    }
    
    private List<TreeNode> generateBSTfrom(int start, int end) {
        List<TreeNode> res = new ArrayList<>();
        if (start > end) {
            res.add(null);
            return res;
        }
        
        for (int i = start; i <= end; i++){
            List<TreeNode> leftChildren = generateBSTfrom(start, i-1);
            List<TreeNode> rightChildren = generateBSTfrom(i + 1, end);
            for (TreeNode left : leftChildren) {
                for (TreeNode right : rightChildren) {
                    TreeNode root = new TreeNode(i);
                    root.left = left;
                    root.right = right;
                    res.add(root);
                }
            }
        }
        return res;
    }
}
```

I had the idea from the question **LC241. Different Ways to Add Parentheses**. We can assume all structurally unique BST of left children and right children of root `i` are generated. Then we just need to combine all possible left children and right children to generate all possible BST heading from a TreeNode with value `i`.

**NOTE** we need to put `null` as leaf TreeNode.

**Complexity:**

* **worst-case time complexity:** O(2<sup>n*n*n</sup>).
* **worst-case space complexity:** O(2<sup>n*n*n</sup>).

I am not very sure if the complexity is correct. It's very high anyway.
