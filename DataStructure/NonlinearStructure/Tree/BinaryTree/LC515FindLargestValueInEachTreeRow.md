# LC515. Find Largest Value in Each Tree Row

### LeetCode

## Question

You need to find the largest value in each row of a binary tree.

**Example:**

```
Input: 

          1
         / \
        3   2
       / \   \  
      5   3   9 

Output: [1, 3, 9]
```

## Solutions

### Solution 1

* C++ (12ms)
```
class Solution {
public:
    void RecursiveLV(TreeNode* root, vector<int>& res, int depth)
    {
        if(root==NULL) return;
        if(depth==res.size()) res.push_back(root->val);
        res[depth] = max(res[depth], root->val);
        RecursiveLV(root->left, res, depth+1);
        RecursiveLV(root->right, res, depth+1);
    }
    vector<int> largestValues(TreeNode* root) {
        vector<int>res;
        RecursiveLV(root, res, 0);
        return res;
    }
};
```

Recursive with the depth of each node. Based on the depth of each node, compare and select the maximum value of each layer.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the number of nodes in the tree `root`.
* **worst-case space complexity:** `O(h)`, where `h` is the height of the tree `root`.