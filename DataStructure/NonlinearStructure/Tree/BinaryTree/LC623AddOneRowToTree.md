# LC623. Add One Row to Tree

### LeetCode

## Question

Given the root of a binary tree, then value v and depth d, you need to add a row of nodes with value v at the given depth d. The root node is at depth 1.

**The adding rule is:** given a positive integer depth d, for each NOT null tree nodes N in depth d-1, create two tree nodes with value v as N's left subtree root and right subtree root. And N's original left subtree should be the left subtree of the new left subtree root, its original right subtree should be the right subtree of the new right subtree root. If depth d is 1 that means there is no depth d-1 at all, then create a tree node with value v as the new root of the whole original tree, and the original tree is the new root's left subtree.

**Example 1:**

**Input:** 

A binary tree as following:
```
       4
     /   \
    2     6
   / \   / 
  3   1 5   
```
v = 1

d = 2

**Output:** 
```
       4
      / \
     1   1
    /     \
   2       6
  / \     / 
 3   1   5   
```

**Example 2:**

**Input:** 

A binary tree as following:
```
      4
     /   
    2    
   / \   
  3   1    
```
v = 1

d = 3

**Output:** 
```
      4
     /   
    2
   / \    
  1   1
 /     \  
3       1
```

**Note:**

* The given d is in range [1, maximum depth of the given tree + 1].
* The given binary tree has at least one tree node.

## Solutions

* C++1
```
TreeNode* addOneRow(TreeNode* root, int v, int d) {
        if(d==1)
        {
            TreeNode* newRoot = new TreeNode(v);
            newRoot->left = root;
            return newRoot;
        }
        else if(d==2)
        {
            TreeNode* ln = new TreeNode(v);
            TreeNode* rn = new TreeNode(v);;
            ln->left = root->left;
            rn->right = root->right;
            root->left = ln;
            root->right = rn;
            return root;
        }
        if(root->left != NULL)
            root->left = addOneRow(root->left, v, d-1);
        if(root->right != NULL)
            root->right = addOneRow(root->right, v, d-1);
        return root;
    }
```

## Explanation

It is a typical tree question. Normally, the solusion is recursive.

**clear the Adding rules:**

1. Adding to the root layer: create a tree node with value `v` as the new root of the whole original tree, and the original tree is the new root's left subtree.
2. Adding to the mid layer: create two tree nodes with value v as N's left subtree root and right subtree root. And N's original left subtree should be the left subtree of the new left subtree root, its original right subtree should be the right subtree of the new right subtree root.
3. Adding to the leaves layer: create two tree nodes with value v as N's left subtree root and right subtree root. We can assume N's original left and right subtrees are NULL Nodes, and put the two NULL Nodes to the two created tree Nodes.

**Note:** It may be not full tree, should check if the Node is NULL.

* **worst-case time complexity:** O(log(n))
* **worst-case space complexity:** O(n)

## Experiences:

1. Always be careful the possible NULL nodes
2. Don't assume the tree is full tree, balanced tree or Binary Search tree if the question didn't define it.
3. depth defined 
