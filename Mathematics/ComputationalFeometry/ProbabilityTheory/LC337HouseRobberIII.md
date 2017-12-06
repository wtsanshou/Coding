# LC337. House Robber III

### LeetCode

## Question

The thief has found himself a new place for his thievery again. There is only one entrance to this area, called the "root." Besides the root, each house has one and only one parent house. After a tour, the smart thief realized that "all houses in this place forms a binary tree". It will automatically contact the police if two directly-linked houses were broken into on the same night.
Determine the maximum amount of money the thief can rob tonight without alerting the police.

**Example 1:**

```
     3
    / \
   2   3
    \   \ 
     3   1
```

Maximum amount of money the thief can rob = 3 + 3 + 1 = 7.

**Example 2:**

```
     3
    / \
   4   5
  / \   \ 
 1   3   1
```

Maximum amount of money the thief can rob = 4 + 5 = 9.

## Solutions

* C++1 (16ms)
```
class Solution {
public:
    vector<int> robBT(TreeNode* root)
    {
        vector<int> curNext(2);
        if(root==NULL) return curNext;
        vector<int> left = robBT(root->left);
        vector<int> right = robBT(root->right);
        curNext[0] = root->val + left[1] + right[1]; //rob current layer
        curNext[1] = max(left[0], left[1]) + max(right[0], right[1]);
        return curNext;
    }
    int rob(TreeNode* root) {
        vector<int>res = robBT(root);
        return max(res[0], res[1]);
    }
};
```

* Java1 (1ms)
```
public class Solution {
    public int rob(TreeNode root) {
        int[] rebSum = robTree(root);
        return Math.max(rebSum[0], rebSum[1]);
    }
    
    private int[] robTree(TreeNode root)
    {
        int[] robSum = new int[2];
        if(root==null) return robSum;
        int[] robLeft = robTree(root.left);
        int[] robRight = robTree(root.right);
        robSum[0] = Math.max(robLeft[0], robLeft[1]) 
                  + Math.max(robRight[0], robRight[1]);
        robSum[1] = root.val + robLeft[0] + robRight[0];
        return robSum;
    }
}
```

## Explanation

Using an array, arr[0] store robbing from the current layer of the node, arr[1] store robbing from the next layer of the node. 

It's more clear to create a struct to store them.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(n)