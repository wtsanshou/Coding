# LC872. Leaf-Similar Trees

### LeetCode

## Question

Consider all the leaves of a binary tree.  From left to right order, the values of those leaves form a leaf value sequence.

![LC872. Leaf-Similar Trees](Images/LC872Leaf-SimilarTrees.png)

For example, in the given tree above, the leaf value sequence is (6, 7, 4, 9, 8).

Two binary trees are considered leaf-similar if their leaf value sequence is the same.

Return true if and only if the two given trees with head nodes root1 and root2 are leaf-similar.

**Note:**

* Both of the given trees will have between 1 and 100 nodes.

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
    def leafSimilar(root1: TreeNode, root2: TreeNode): Boolean = {
        val l1 = getLeaves(root1)
        val l2 = getLeaves(root2)
        l1 == l2
    }
    
    def getLeaves(root: TreeNode): List[Int] = {
        if(root == null) return null
        if(root.left == null && root.right == null) return List(root.value)
        if(root.left == null) return getLeaves(root.right)
        if(root.right == null) return getLeaves(root.left)
        getLeaves(root.left) ::: getLeaves(root.right)
    }
}
```

## Explanation

Get both leaf value sequences and compare them.

* **worst-case time complexity:** `O(N)`,  where `N` is the number of nodes in the tree.
* **worst-case space complexity:** `O(N)`,  where `N` is the number of nodes in the tree.
