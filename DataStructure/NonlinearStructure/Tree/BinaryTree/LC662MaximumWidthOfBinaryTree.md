# LC662. Maximum Width of Binary Tree

### LeetCode

## Question

Given a `binary tree`, write a function to get the maximum width of the given tree. The width of a tree is the maximum width among all levels. The binary tree has the same structure as a full binary tree, but some nodes are null.

The width of one level is defined as the length between the end-nodes (the leftmost and right most non-null nodes in the level, where the null nodes between the end-nodes are also counted into the length calculation.

**Example 1:**
```
Input: 

           1
         /   \
        3     2
       / \     \  
      5   3     9 

Output: 4
Explanation: The maximum width existing in the third level with the length 4 (5,3,null,9).
```

**Example 2:**
```
Input: 

          1
         /  
        3    
       / \       
      5   3     

Output: 2
Explanation: The maximum width existing in the third level with the length 2 (5,3).
```

**Example 3:**
```
Input: 

          1
         / \
        3   2 
       /        
      5      

Output: 2
Explanation: The maximum width existing in the second level with the length 2 (3,2).
```

**Example 4:**
```
Input: 

          1
         / \
        3   2
       /     \  
      5       9 
     /         \
    6           7
Output: 8
Explanation:The maximum width existing in the fourth level with the length 8 (6,null,null,null,null,null,null,7).
```

**Note:** Answer will in the range of 32-bit signed integer.

## Solutions

* Java1
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
class Solution {
    
    private MinMaxPair[] minMaxPairs;
    
    public int widthOfBinaryTree(TreeNode root) {
        int depth = getDepth(root);
        minMaxPairs = new MinMaxPair[depth];
        if(root == null) return 0;
        findMinMaxInAllLayer(root.left, -1, 0);
        findMinMaxInAllLayer(root.right, 1, 0);
        return getTheMaxWidth();
    }
    
    private int getDepth(TreeNode root){
        if(root == null) return 0;
        return Math.max(getDepth(root.left)+1, getDepth(root.right)+1);
    }
    
    private void findMinMaxInAllLayer(TreeNode root, int distance, int depth){
        if(root == null) return;
        if(minMaxPairs[depth] == null) minMaxPairs[depth] = new MinMaxPair();
        minMaxPairs[depth].adjustMinMax(distance);
        
        int newDistance = distance*2;
        findMinMaxInAllLayer(root.left,  newDistance - (isInTheLeftOfRoot(distance) ? 0 : 1), depth+1);
        findMinMaxInAllLayer(root.right, newDistance + (isInTheLeftOfRoot(distance) ? 1 : 0), depth+1);
        
    }
    
    private boolean isInTheLeftOfRoot(int distance){
        return distance < 0;
    }
    
    private int getTheMaxWidth(){
        int result = 1;
        for(int i=0; i<minMaxPairs.length; ++i){
            if(minMaxPairs[i] != null){
                result = Math.max(result, minMaxPairs[i].max - minMaxPairs[i].min + ((isInTheSameSide(i)) ? 1 : 0));
            }
        }
        return result;
    }
    
    private boolean isInTheSameSide(int i){
        return minMaxPairs[i].max * minMaxPairs[i].min > 0;
    }
}

class MinMaxPair{
    public int min;
    public int max;
    public MinMaxPair(){
        this.min = Integer.MAX_VALUE;
        this.max = Integer.MIN_VALUE;
    }
    
    public void adjustMinMax(int value){
        min = Math.min(min, value);
        max = Math.max(max, value);
    }
}
```

## Explanation

The idea is to find out the distance between each node and the middle of the tree. 

For example:

```
                 0
          /      |      \
        -1       |       1
       /  \      |     /   \    
    -2     -1    |    1     2
    / \   /   \  |  /   \  /  \
 -4   -3 -2   -1 | 1     2 3   4
.   .   .   .   .   .   .   .   .   .
```

For each layer, only keep the most left and the most right nodes' distances.

Finally, check each layer, find the maximum width of the binary tree.

**Corner cases:**

1. Empty tree.
2. Only one node tree.
3. Only one leg tree.
4. The maximum width nodes are all in the left or all in the right of the tree. We need add `1` to the result.
5. `Answer will in the range of 32-bit signed integer` does **not** mean that the depth of the tree is limited.

* **worst-case time complexity:** `O(N)`,  where `N` is the number of nodes in the tree.
* **worst-case space complexity:** `O(H)`, where `H` is the height of the tree. Our recursive call stack could be up to `H` layers deep.
