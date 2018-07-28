# LC559. Maximum Depth of N-ary Tree

### LeetCode

## Questions

Given a n-ary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

For example, given a 3-ary tree:

![LC559. Maximum Depth of N-ary Tree](images/LC559MaximumDepthOfN-aryTree.png)
 
We should return its max depth, which is 3.

**Note:**

* The depth of the tree is at most 1000.
* The total number of nodes is at most 5000.

## Solutions

* Java1
```
/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val,List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/
class Solution {
    public int maxDepth(Node root) {
        if(root == null) return 0;
        int res = 0;
        for(Node node : root.children)
            res = Math.max(res, maxDepth(node));
        return res + 1;
    }
}
```

# Explanation

Solve it from leaf nodes.

* **worst-case time complexity:** O(log(n)), where n is the number of the nodes in the tree.
* **worst-case space complexity:** O(log(n)), where n is the number of the nodes in the tree.
