# LC513. Find Bottom Left Tree Value

### LeetCode

## Question

Given a binary tree, find the leftmost value in the last row of the tree.

**Example 1:**

```
Input:

    2
   / \
  1   3

Output:
1
```

**Example 2:**

```
Input:

        1
       / \
      2   3
     /   / \
    4   5   6
       /
      7

Output:
7
```

**Note: **

* You may assume the tree (i.e., the given root node) is not NULL.

## Solutions

### Solution 1

* C++ (12ms)
```
class Solution {
public:
    void RescursiveBL(TreeNode* root, vector<int>& res, int depth)
    {
        if(root==NULL) return;
        if(res.size() == depth) res.push_back(root->val);
        RescursiveBL(root->left, res, depth+1);
        RescursiveBL(root->right, res, depth+1);
    }
    int findBottomLeftValue(TreeNode* root) {
        vector<int> res;
        RescursiveBL(root, res, 0);
        return res.back();
    }
};
```

`res.size() == depth` means only push the left side nodes into the vector `res`.

### Solution 2

1. Find the depth of the tree.
2. Recursive the tree, when reach the depth of the tree, return the node.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the number of nodes in the tree `root`.
* **worst-case space complexity:** `O(n)`, where `n` is the number of nodes in the tree `root`.