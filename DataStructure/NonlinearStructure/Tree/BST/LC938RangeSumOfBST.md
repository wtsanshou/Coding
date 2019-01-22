# LC938. Range Sum of BST

### LeetCode

## Question

Given the root node of a binary search tree, return the sum of values of all nodes with value between L and R (inclusive).

The binary search tree is guaranteed to have unique values.

**Example 1:**
```
Input: root = [10,5,15,3,7,null,18], L = 7, R = 15
Output: 32
```

**Example 2:**
```
Input: root = [10,5,15,3,7,13,18,1,null,6], L = 6, R = 10
Output: 23
```

**Note:**

* The number of nodes in the tree is at most 10000.
* The final answer is guaranteed to be less than 2^31.

## Solutions

* Scala1
```
def rangeSumBST(root: TreeNode, L: Int, R: Int): Int = {
    if(root==null) 0
    else if(root.value >= L && root.value <= R) root.value + rangeSumBST(root.left, L, R) + rangeSumBST(root.right, L, R)
    else rangeSumBST(root.left, L, R) + rangeSumBST(root.right, L, R)
}
```

## Explanation

* **worst-case time complexity:** O(log(n))
* **worst-case space complexity:** O(1)
