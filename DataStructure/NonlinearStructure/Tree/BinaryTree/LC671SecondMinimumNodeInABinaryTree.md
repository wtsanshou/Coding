# LC671. Second Minimum Node In a Binary Tree

### LeetCode

## Question

Given a non-empty special binary tree consisting of nodes with the non-negative value, where each node in this tree has exactly two or zero sub-node. If the node has two sub-nodes, then this node's value is the smaller value among its two sub-nodes.

Given such a binary tree, you need to output the second minimum value in the set made of all the nodes' value in the whole tree.

If no such second minimum value exists, output -1 instead.

**Example 1:**

```
Input: 

    2
   / \
  2   5
     / \
    5   7

Output: 5
```

**Explanation:** 

The smallest value is 2, the second smallest value is 5.

**Example 2:**

```
Input: 

    2
   / \
  2   2

Output: -1
```

**Explanation:** 

The smallest value is 2, but there isn't any second smallest value.

## Solutions

* C#1
```
public class Solution {
    
    private int max = 0;
    private int rootVal = 0;
    
    public int FindSecondMinimumValue(TreeNode root) {
        max = getMax(root);
        if(max == root.val) return -1;
        rootVal = root.val;
        checkSecondMin(root);
        return max;
    }
    
    private int getMax(TreeNode root){
        if(root == null) return 0;
        if(root.left == null) return root.val;
        return Math.Max(getMax(root.left), getMax(root.right));
    }
    
    private void checkSecondMin(TreeNode root){
        if(root == null) return;
        if(root.left == null){
            if(root.val != rootVal)
                max = Math.Min(max, root.val);
            return;
        }
        if(root.left.val == root.right.val){
            checkSecondMin(root.left);
            checkSecondMin(root.right);
        }
        else if(root.left.val == rootVal){
            max = Math.Min(max, root.right.val);
            checkSecondMin(root.left);
        }
        else{
            max = Math.Min(max, root.left.val);
            checkSecondMin(root.right);
        }
    }
}
```

## Explanation

Find the max value of the binary tree.

1. The second minimum value of the binary tree will not be in the subtree of a node which is not equal to root value.
2. Only check the subtree of the nodes which are queal to root value.
3. Cut the tree which are not equal to the root value, but check the node's value to get the second minimum value of the whole tree.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(h)
