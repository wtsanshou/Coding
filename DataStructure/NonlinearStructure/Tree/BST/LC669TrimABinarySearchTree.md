# LC669. Trim a Binary Search Tree 

### LeetCode

## Question

 Given a binary search tree and the lowest and highest boundaries as L and R, trim the tree so that all its elements lies in [L, R] (R >= L). You might need to change the root of the tree, so the result should return the new root of the trimmed binary search tree.

**Example 1:**

**Input:** 
```
    1
   / \
  0   2

  L = 1
  R = 2
```

**Output:** 
```
    1
      \
       2
```

**Example 2:**

**Input:** 
```
    3
   / \
  0   4
   \
    2
   /
  1

  L = 1
  R = 3
```

**Output:** 
```
      3
     / 
   2   
  /
 1
```

## Solution

* C++1
```
TreeNode* trimBST(TreeNode* root, int L, int R) {
    if(root == NULL) return NULL;
    if(root->val < L)
    {
        root = root->right;
        return trimBST(root, L, R);
    }
    if(root->val > R)
    {
        root = root->left;
        return trimBST(root, L, R);
    }
    if(root->val == L) root->left = NULL;
    if(root->val == R) root->right = NULL;
    root->left = trimBST(root->left, L, R);
    root->right = trimBST(root->right, L, R);
    return root;
}
```

## Explanation

Four corner cases:
1. `root->val < L`, root and left child of root should be removed, but right child of root might be valid.
2. `root->val > R`, root and right child of root should be removed, but left child of root might be valid.
3. `root->val == L`, left child of root should be removed.
4. `root->val == R`, right child of root should be removed.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(h)