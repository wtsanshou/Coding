# LC230. Kth Smallest Element in a BST

### LeetCode

## Question

Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.

**Note:**

* You may assume k is always valid, 1 ≤ k ≤ BST's total elements.

**Follow up:**

What if the BST is modified (insert/delete operations) often and you need to find the kth smallest frequently? How would you optimize the kthSmallest routine?

## Solutions

### Solution 1

* C++ (12ms) 
```
class Solution {
public:
    int countNodes(TreeNode* root)
    {
        if(root==NULL) return 0;
        return countNodes(root->left) + countNodes(root->right) + 1;
    }
    int kthSmallest(TreeNode* root, int k) {
        int leftSum = countNodes(root->left) + 1;
        if(leftSum == k) return root->val;
        else if(leftSum > k) return kthSmallest(root->left, k);
        else return kthSmallest(root->right, k-leftSum);
    }
};
```

* Java
```
public class Solution {
    public int kthSmallest(TreeNode root, int k) {
        if(root == null) return 0;
        int count = countNodes(root.left);
        if(count == k-1)  
            return root.val;
        else if(count >= k)
            return kthSmallest(root.left, k);
        else 
            return kthSmallest(root.right, k-count-1);
    }
    
    private int countNodes(TreeNode root)
    {
        if(root == null) return 0;
        return 1 + countNodes(root.left) + countNodes(root.right);
    }
}
```

Count the number `count` of the left subtree.

1. if `count == k-1`, the root value is the kth smallest element.
2. if `count > k-1`, the kth smallest element is in the left subtree.
3. if `count < k-1`, the kth smallest element is the `k-count-1`th smallest element in the right subtree.

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is the number of nodes in the tree `root`.
* **worst-case space complexity:** `O(h)`, where `h` is the height of the tree `root`.

### Solution 2

* C++
```
class Solution {
public:
    int kthSmallestHelper(TreeNode* root, int& k)
    {
        if(root==NULL) return -1;
        int x = kthSmallestHelper(root->left, k);
        if(k==0) return x;
        if(--k==0) return root->val;
        return kthSmallestHelper(root->right, k);
    }
    int kthSmallest(TreeNode* root, int k) {
        return kthSmallestHelper(root,k);
    }
};
```

* C++
```
int kthSmallest(TreeNode* root, int k) {
    stack<TreeNode*> s;
    int count=0;
    TreeNode* t = root;
    while(t!=NULL || !s.empty())
    {
        if(t != NULL)
        {
            s.push(t);
            t = t->left;
        }
        else
        {
            t = s.top();
            s.pop();
            if(++count == k) return t->val;
            t = t->right;
        }
    }
    return 0;
}
```

Count from the smallest element in the tree until count to the kth smallest element.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the number of nodes in the tree `root`.
* **worst-case space complexity:** `O(h)`, where `h` is the height of the tree `root`.

### Solution 3

**Hint:**

1.  Try to utilize the property of a BST.
2.  What if you could modify the BST node's structure?
3.  The optimal runtime complexity is O(height of BST).
