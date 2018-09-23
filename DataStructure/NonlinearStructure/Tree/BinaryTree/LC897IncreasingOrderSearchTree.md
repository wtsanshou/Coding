# LC897. Increasing Order Search Tree

### LeetCode

## Question

Given a tree, rearrange the tree in **in-order** so that the leftmost node in the tree is now the root of the tree, and every node has no left child and only 1 right child.

**Example 1:**
```
Input: [5,3,6,2,4,null,8,1,null,null,null,7,9]

       5
      / \
    3    6
   / \    \
  2   4    8
 /        / \ 
1        7   9

Output: [1,null,2,null,3,null,4,null,5,null,6,null,7,null,8,null,9]

 1
  \
   2
    \
     3
      \
       4
        \
         5
          \
           6
            \
             7
              \
               8
                \
                 9  
```

**Note:**

* The number of nodes in the given tree will be between 1 and 100.
* Each node will have a unique integer value from 0 to 1000.

## Solutions

* Scala1
```
/**
 * Definition for a binary tree node.
 * class TreeNode(var _value: Int) {
 *   var value: Int = _value
 *   var left: TreeNode = null
 *   var right: TreeNode = null
 * }
 */
object Solution {
    def increasingBST(root: TreeNode): TreeNode = {
        val res = getIncreasingBST(root)
        res(0)
    }
    
    def getIncreasingBST(root: TreeNode): List[TreeNode] = {
        if(root.left==null && root.right==null) return List(root, root)
        if(root.left==null){
            var right = getIncreasingBST(root.right)
            root.right = right(0)
            return List(root, right(1))
        }
        if(root.right==null){
            var left = getIncreasingBST(root.left)
            left(1).right = root
            root.left = null
            return List(left(0), root)
        }
        var left = getIncreasingBST(root.left)
        var right = getIncreasingBST(root.right)
        left(1).right = root
        root.right = right(0)
        root.left = null
        List(left(0), right(1))
    }
}
```

* Scala2
```
object Solution {
    def increasingBST(root: TreeNode): TreeNode = {
        getIncreasingBST(root)._1
    }
    
    def getIncreasingBST(root: TreeNode): (TreeNode, TreeNode)= {
        if(root.left==null && root.right==null) return (root, root)
        if(root.left==null){
            val (rightL, rightR) = getIncreasingBST(root.right)
            root.right = rightL
            return (root, rightR)
        }
        if(root.right==null){
            val (leftL, leftR) = getIncreasingBST(root.left)
            leftR.right = root
            root.left = null
            return (leftL, root)
        }
        val (leftL, leftR) = getIncreasingBST(root.left)
        val (rightL, rightR)  = getIncreasingBST(root.right)
        leftR.right = root
        root.right = rightL
        root.left = null
        (leftL, rightR)
    }
}
```

* Scala3
```
object Solution {
    
    var cur = new TreeNode(0)
    
    def increasingBST(root: TreeNode): TreeNode = {
        var res = new TreeNode(0)
        cur = res
        inOrder(root)
        res.right
    }
    
    def inOrder(root: TreeNode): Unit = {
        if(root==null) return
        inOrder(root.left)
        cur.right = root
        cur = root
        root.left = null
        inOrder(root.right)
    }
}
```

* Java1
```
class Solution {
    
    public TreeNode increasingBST(TreeNode root) {
        TreeNode[] res = getIncreasingBST(root);
        return res[0];
    }
    
    private TreeNode[] getIncreasingBST(TreeNode root) {
        if(root.left==null && root.right==null) return new TreeNode[] {root, root};
        if(root.left==null) {
            TreeNode[] right = getIncreasingBST(root.right);
            root.right = right[0];
            return new TreeNode[] {root, right[1]};
        }
        if(root.right==null){
            TreeNode[] left = getIncreasingBST(root.left);
            left[1].right=root;
            root.left = null;
            return new TreeNode[] {left[0], root};
        }
        TreeNode[] left = getIncreasingBST(root.left);
        TreeNode[] right = getIncreasingBST(root.right);
        left[1].right = root;
        root.right = right[0];
        root.left = null;
        return new TreeNode[] {left[0], right[1]};
    }
}
```

## Explanation

Don't be fooled by the example. The question is not to sort the tree.

`Each node will have a unique integer value from 0 to 1000.` is no use for this question.

Two ideas:

1. recursive both children, return their head and tail.
2. inorder traversal

* **worst-case time complexity:** O(log(n)), where `n` is the number of the tree.
* **worst-case space complexity:** O(log(n)), where `n` is the number of the tree.

