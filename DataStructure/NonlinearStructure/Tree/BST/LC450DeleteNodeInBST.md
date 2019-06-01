# LC450. Delete Node in a BST

### LeetCode

## Question

Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return the root node reference (possibly updated) of the BST.

Basically, the deletion can be divided into two stages:

1.	Search for a node to remove.
2.	If the node is found, delete the node.

**Note:** Time complexity should be O(height of tree).

**Example:**
```
root = [5,3,6,2,4,null,7]
key = 3

    5
   / \
  3   6
 / \   \
2   4   7

Given key to delete is 3. So we find the node with value 3 and delete it.

One valid answer is [5,4,6,2,null,null,7], shown in the following BST.

    5
   / \
  4   6
 /     \
2       7

Another valid answer is [5,2,6,null,4,null,7].

    5
   / \
  2   6
   \   \
    4   7
```

## Solutions

### Solution 1

* C++ (56ms)
```
class Solution {
public:
    TreeNode* maxOf(TreeNode* root)
    {
        while(root->right != NULL) root = root->right;
        return root;
    }
    TreeNode* deleteNode(TreeNode* root, int key) {
        if(root==NULL) return NULL;
        if(root->val > key)
            root->left = deleteNode(root->left, key);
        else if(root->val < key)
            root->right = deleteNode(root->right, key);
        else 
        {
            if(root->left == NULL) return root->right;
            if(root->right == NULL) return root->left;
            root->val = maxOf(root->left)->val;
            root->left = deleteNode(root->left, root->val);
        }
        return root;
    }
};
```

* C++
```
class Solution {
public:
    int minValOf(TreeNode* root)
    {
        while(root->left != NULL) root = root->left;
        return root->val;
    }
    TreeNode* deleteNode(TreeNode* root, int key) {
        if(root==NULL) return NULL;
        if(key < root->val)
            root->left = deleteNode(root->left, key);
        else if(key > root->val)
            root->right = deleteNode(root->right, key);
        else
        {
            if(root->left == NULL)
                return root->right;
            if(root->right ==NULL)
                return root->left;
            root->val = minValOf(root->right);
            root->right = deleteNode(root->right, root->val);
        }
        return root;
    }
};
```

1. Find the node where it need to be deleted.
2. Replace the value with the maximum (or minimum) nodes `k` in the left (or right) subtree.
3. Recursive into the substree to deleted the node with value `k`

**Complexity:**

* **worst-case time complexity:** `O(h)`, where `h` is the height of the tree `root`.
* **worst-case space complexity:** `O(h)`, where `h` is the height of the tree `root`.
