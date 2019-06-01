# LC235. Lowest Common Ancestor of a Binary Search Tree

### LeetCode

## Question

Given a binary search tree (BST), find the lowest common ancestor (LCA) of two given nodes in the BST.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes v and was the lowest node in T that has both v and was descendants (where we allow a node to be a descendant of itself).”

```
        _______6______
       /              \
    ___2__          ___8__
   /      \        /      \
   0      _4       7       9
         /  \
         3   5
```

For example, the lowest common ancestor (LCA) of nodes 2 and 8 is 6. Another example is LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself according to the LCA definition.

## Solutions

### Solution 1
* C++ (26ms, beats 91.83%)
```
TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    if(root==NULL || p==NULL || q==NULL) return NULL;
    if((root->val - p->val)*(root->val - q->val) <= 0) return root;
    else if(root->val > p->val)
        return lowestCommonAncestor(root->left, p, q);
    else
        return lowestCommonAncestor(root->right, p, q);
}
```

**3 cases:**

1. Both nodes' values are less than the root's value, check the left subtree.
2. Both nodes' values are larger than the root's value, check the right subtree.
3. One node is less or equal than the root's value, the other node is larger or equal than the root's value, return the root

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the number of nodes in the tree `root`.
* **worst-case space complexity:** `O(h)`, where `h` is the height of the tree `root`.
