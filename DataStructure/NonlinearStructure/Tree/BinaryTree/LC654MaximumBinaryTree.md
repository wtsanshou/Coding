# LC654. Maximum Binary Tree

### LeetCode

## Question

Given an integer array with no duplicates. A maximum tree building on this array is defined as follow:

* The root is the maximum number in the array.
* The left subtree is the maximum tree constructed from left part subarray divided by the maximum number.
* The right subtree is the maximum tree constructed from right part subarray divided by the maximum number.

Construct the maximum tree by the given array and output the root node of this tree.

**Example 1:**

**Input:**


`[3,2,1,6,0,5]`


**Output:** return the tree root node representing the following tree:

```
      6
    /   \
   3     5
    \    / 
     2  0   
       \
        1
```

**Note:**

The size of the given array will be in the range [1,1000].

## Solutions

* C#1 (Beat 96.84%)
```
public class Solution {
    public TreeNode ConstructMaximumBinaryTree(int[] nums) {
        return GetMaximumNode(nums, 0, nums.Length-1);
    }
    
    private TreeNode GetMaximumNode(int[] nums, int start, int end){
        if(start > end) return null;
        if(start == end) return new TreeNode(nums[start]);
        int max = Int32.MinValue, mid = start;
        for(int i=start; i<=end; ++i){
            if(nums[i] > max){
                max = nums[i];
                mid = i;
            }
        }
        TreeNode root = new TreeNode(max);
        root.left = GetMaximumNode(nums, start, mid-1);
        root.right = GetMaximumNode(nums, mid+1, end);
        return root;
    }
}
```

## Explanation

1. Find the maximum value in the array as a node `root`.
2. Recursive to the left side of the maximum value as left child of the node `root`.
3. Recursive to the right side of the maximum value as right child of the node `root`.

* **worst-case time complexity:** O(n<sup>2</sup>)
* **worst-case space complexity:** O(n)
