# LC116. Populating Next Right Pointers in Each Node

### LeetCode

## Question

Given a binary tree

```
struct TreeLinkNode {
  TreeLinkNode *left;
  TreeLinkNode *right;
  TreeLinkNode *next;
}
```

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.

Initially, all next pointers are set to NULL.

**Note:**

* You may only use constant extra space.
* You may assume that it is a perfect binary tree (ie, all leaves are at the same level, and every parent has two children).

For example,  Given the following perfect binary tree,

```
         1
       /  \
      2    3
     / \  / \
    4  5  6  7
```

After calling your function, the tree should look like:

```
         1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \  / \
    4->5->6->7 -> NULL
```

## Solutions

* C++1
```
void connect(TreeLinkNode *root) {
    if(root==NULL) return;
    if(root->left != NULL)
    {
        root->left->next = root->right;
        if(root->next != NULL)
            root->right->next = root->next->left;
    }
    connect(root->left);
    connect(root->right);
}
```

* C++2
```
void connect(TreeLinkNode *root) {
    if(root==NULL) return;
    TreeLinkNode *pre = root; 
    TreeLinkNode *cur;
    while(pre->left!=NULL)
    {
        cur = pre;
        while(cur!=NULL)
        {
            cur->left->next = cur->right;
            if(cur->next != NULL)
            {
                cur->right->next = cur->next->left;
            }
            cur = cur->next;
        }
        pre = pre->left;
    }
}
```

## Explanation

Recursive and iteration solutions. 

For each node, connect its left child to its right child, connect its right child to its next node's left child.

* **worst-case time complexity:** O(n)

**Iteration**

* **worst-case space complexity:** O(1)

**Recursive**

* **worst-case space complexity:** O(log(n))
