# LC530. Minimum Absolute Difference in BST

### LeetCode

## Question

Given a binary search tree with non-negative values, find the minimum absolute difference between values of any two nodes.

**Example:**
```
Input:

   1
    \
     3
    /
   2

Output:
1
```

**Explanation:**

The minimum absolute difference is 1, which is the difference between 2 and 1 (or between 2 and 3).

## Solutions

### Solution 1
* C++ (16ms)
```
class Solution {
public:
    int getMaxFromLeftNode(TreeNode* root)
    {
        while(root->right!=NULL) root=root->right;
        return root->val;
    }
    int getMinFromRightNode(TreeNode* root)
    {
        while(root->left!=NULL) root=root->left;
        return root->val;
    }
    int getMinimumDifference(TreeNode* root) {
        if(root==NULL) return INT_MAX;
        int LD = (root->left!=NULL) ? root->val - getMaxFromLeftNode(root->left) : INT_MAX;
        int RD = (root->right!=NULL) ? getMinFromRightNode(root->right) - root->val : INT_MAX;
        return min(min(LD, RD), min(getMinimumDifference(root->left), getMinimumDifference(root->right)));
    }
};
```

The minimum absolute difference must be the adjacent values of the sorted nodes, that is to say we need to compare each node with the maximum value of its left children and the minimum value of its right children. 

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is the number of nodes in the tree `root`.
* **worst-case space complexity:** `O(h)`, where `h` is the height of the tree `root`.
