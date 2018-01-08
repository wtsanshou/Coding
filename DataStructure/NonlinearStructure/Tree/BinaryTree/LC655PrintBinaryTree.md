# LC655. Print Binary Tree

### LeetCode

## Question

Print a binary tree in an m*n 2D string array following these rules:

The row number m should be equal to the height of the given binary tree.

The column number n should always be an odd number.

The root node's value (in string format) should be put in the exactly middle of the first row it can be put. The column and the row where the root node belongs will separate the rest space into two parts (left-bottom part and right-bottom part). You should print the left subtree in the left-bottom part and print the right subtree in the right-bottom part. The left-bottom part and the right-bottom part should have the same size. Even if one subtree is none while the other is not, you don't need to print anything for the none subtree but still need to leave the space as large as that for the other subtree. However, if two subtrees are none, then you don't need to leave space for both of them.

Each unused space should contain an empty string "".

Print the subtrees following the same rules.

**Example 1:**

**Input:**

```
     1
    /
   2
```

**Output:**

```
[["", "1", ""],
 ["2", "", ""]]
```

**Example 2:**

**Input:**

```
     1
    / \
   2   3
    \
     4
```

**Output:**

```
[["", "", "", "1", "", "", ""],
 ["", "2", "", "", "", "3", ""],
 ["", "", "4", "", "", "", ""]]
```

**Example 3:**

**Input:**

```
      1
     / \
    2   5
   / 
  3 
 / 
4 
```

**Output:**

```
[["",  "",  "", "",  "", "", "", "1", "",  "",  "",  "",  "", "", ""]
 ["",  "",  "", "2", "", "", "", "",  "",  "",  "",  "5", "", "", ""]
 ["",  "3", "", "",  "", "", "", "",  "",  "",  "",  "",  "", "", ""]
 ["4", "",  "", "",  "", "", "", "",  "",  "",  "",  "",  "", "", ""]]
```

**Note:** The height of binary tree is in the range of [1, 10].

## Solutions

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
```

* Java1 (9ms)
```
class Solution {
    public List<List<String>> printTree(TreeNode root) {
        int h = getDepth(root);
        int w = (int)Math.pow(2, h) - 1;
        List<List<String>> res = new ArrayList<>();
        for(int i=0; i<h; ++i){
            List<String> row = new ArrayList<>();
            for(int j=0; j<w; ++j)
                row.add("");
            res.add(row);
        }
        putTreeIn(res, root, 0, w, 0);
        return res;
    }
    
    private int getDepth(TreeNode root){
        if(root == null) return 0;
        return 1 + Math.max(getDepth(root.left), getDepth(root.right));
    }
    
    private void putTreeIn(List<List<String>> res, TreeNode root, int left, int right, int depth){
        if(root == null) return;
        int mid = (left + right) / 2;
        res.get(depth).set(mid, String.valueOf(root.val));
        putTreeIn(res, root.left, left, mid, depth+1);
        putTreeIn(res, root.right, mid+1, right, depth+1);
    }
}
```

* Java2 (85ms)
```
class Solution {
    public List<List<String>> printTree(TreeNode root) {
        int h = getDepth(root);
        int w = (int)Math.pow(2, h) - 1;
        String[][] res = new String[h][w];
        for(int i=0; i<h; ++i)
            Arrays.fill(res[i], "");
        putTreeIn(res, root, 0, w, 0);
        return Arrays.stream(res)
                     .map(Arrays::asList)
                     .collect(Collectors.toList());
    }
    
    private int getDepth(TreeNode root){
        if(root == null) return 0;
        return 1 + Math.max(getDepth(root.left), getDepth(root.right));
    }
    
    private void putTreeIn(String[][] res, TreeNode root, int left, int right, int depth){
        if(root == null) return;
        int mid = (left + right) / 2;
        res[depth][mid] = String.valueOf(root.val);
        putTreeIn(res, root.left, left, mid, depth+1);
        putTreeIn(res, root.right, mid+1, right, depth+1);
    }
}
```

## Explanation

Each node should print at the middle between its most left possible child and its most right possible child.

We know the layer number when we do recursive. We can find the children location range of the current node from the node's parent location and parent's children location range.

* **worst-case time complexity:** O(h * 2<sup>h</sup>)
* **worst-case space complexity:** O(h * 2<sup>h</sup>)