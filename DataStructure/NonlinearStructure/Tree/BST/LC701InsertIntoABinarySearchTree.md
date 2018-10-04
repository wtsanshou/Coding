# LC701. Insert into a Binary Search Tree

### LeetCode

## Question

Given the root node of a binary search tree (BST) and a value to be inserted into the tree, insert the value into the BST. Return the root node of the BST after the insertion. It is guaranteed that the new value does not exist in the original BST.

Note that there may exist multiple valid ways for the insertion, as long as the tree remains a BST after insertion. You can return any of them.

**For example**

Given the tree:
```
        4
       / \
      2   7
     / \
    1   3
```

And the value to insert: 5

You can return this binary search tree:
```
         4
       /   \
      2     7
     / \   /
    1   3 5
```
This tree is also valid:
```
         5
       /   \
      2     7
     / \   
    1   3
         \
          4
```

## Solutions

* Java1
```
class Solution {
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if(root == null) return new TreeNode(val);
        insertBST(root, val);
        return root;
    }
    
    private void insertBST(TreeNode root, int val){
        if(val < root.val){
            if(root.left == null) root.left = new TreeNode(val);
            else insertBST(root.left, val);
        }
        else{
            if(root.right == null) root.right = new TreeNode(val);
            else insertBST(root.right, val);
        }
    }
}
```

* Scala1
```
def insertIntoBST(root: TreeNode, value: Int): TreeNode = {
    if(root==null) return new TreeNode(value)
    if(root.value > value) root.left = insertIntoBST(root.left, value)
    else root.right = insertIntoBST(root.right, value)
    root
}
```

## Explanation

Insert it to the leaf. It just like find the node in the BST.

* **worst-case time complexity:** O((log(n))<sup>2</sup>), where `n` is the number of nodes in the BST.
* **worst-case space complexity:** O((log(n))<sup>2</sup>), where `n` is the number of nodes in the BST.
