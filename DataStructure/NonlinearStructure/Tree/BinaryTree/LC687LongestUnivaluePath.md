# LC687. Longest Univalue Path

### LeetCOde

## Question

Given a binary tree, find the length of the longest path where each node in the path has the same value. This path may or may not pass through the root.

Note: The length of path between two nodes is represented by the number of edges between them.

**Example 1:**

**Input:**
```
              5
             / \
            4   5
           / \   \
          1   1   5
```

**Output:**
```
2
```

**Explanation:** 5 -> 5 -> 5

**Example 2:**

**Input:**

```
              1
             / \
            4   5
           / \   \
          4   4   5
```

**Output:**

```
2
```

**Explanation:** 4 -> 4 -> 4

**Note:** 

The given binary tree has not more than 10000 nodes. The height of the tree is not more than 1000.

## Solutions

* C#1
```
public class Solution {
    
    private int res;
    
    public int LongestUnivaluePath(TreeNode root) {
        res = 0;
        CountOneLeg(root);
        return res;
    }
    
    private int CountOneLeg(TreeNode root){
        if(root == null) return 0;
        int left = CountOneLeg(root.left);
        int right = CountOneLeg(root.right);
        int leftLeg = 0, rightLeg = 0;
        if(root.left != null && root.val == root.left.val)
            leftLeg += left + 1;
        if(root.right!= null && root.val == root.right.val)
            rightLeg += right + 1;
        res = Math.Max(res, leftLeg + rightLeg);
        return Math.Max(leftLeg, rightLeg);
    }
}
```

## Explanation

We can think of any path (of nodes with the same values) as up to two legs extending from it's root.

Specifically, the root of a path will be the unique node such that the parent of that node does not appear in the path, and a leg will be a path where the root only has one child node in the path.

Then, for each node, we want to know what is the longest possible leg extending left, and the longest possible leg extending right.

While we are computing leg lengths, each candidate answer will be the sum of the arrows in both directions from that node. We record these candidate answers and return the best one.

* **worst-case time complexity:** O(n),  where N is the number of nodes in the tree. We process every node once.
* **worst-case space complexity:** O(H), where H is the height of the tree. Our recursive call stack could be up to H layers deep.
