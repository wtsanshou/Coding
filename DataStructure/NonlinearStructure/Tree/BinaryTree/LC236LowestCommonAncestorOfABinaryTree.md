# LC236. Lowest Common Ancestor of a Binary Tree

### LeetCode

## Question

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes v and w as the lowest node in T that has both v and w as descendants (where we allow a node to be a descendant of itself).”

```
        _______3______
       /              \
    ___5__          ___1__
   /      \        /      \
   6      _2       0       8
         /  \
         7   4
```

For example, the lowest common ancestor (LCA) of nodes 5 and 1 is 3. Another example is LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.

## Solutions

### Solution 1 

* C++
```
class Solution {
public:
    TreeNode* searchNode(TreeNode* root, TreeNode* node)
    {
        if(root==NULL|| root==node) return root;
        TreeNode* left = searchNode(root->left, node);
        TreeNode* right = searchNode(root->right, node);
        if(left!=NULL || right != NULL) return node;
        return NULL;
    }
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(root==NULL || root==p || root==q) return root;
        if(searchNode(root->left, p)!=p && searchNode(root->left, q)!=q)
            return lowestCommonAncestor(root->right, p, q);
        else if(searchNode(root->right, p)!=p && searchNode(root->right, q)!=q)
            return lowestCommonAncestor(root->left, p, q);
        return root;
    }
};
```

* C++
```
TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    if(root==NULL || root==p || root==q) return root;
    TreeNode* right = lowestCommonAncestor(root->right, p, q);
    TreeNode* left = lowestCommonAncestor(root->left, p, q);
    return left&&right ? root: left? left: right;
}
```

**3 cases:**

1. Both nodes in the left subtree, check the left subtree.
2. Both nodes in the right subtree, check the right subtree.
3. One node in the left subtree, one node in the right subtree, return the root

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the number of nodes in the tree `root`.
* **worst-case space complexity:** `O(h)`, where `h` is the height of the tree `root`.
