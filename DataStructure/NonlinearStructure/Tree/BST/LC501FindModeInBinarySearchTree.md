# LC501. Find Mode in Binary Search Tree

### LeetCode

## Question

Given a binary search tree (BST) with duplicates, find all the mode(s) (the most frequently occurred element) in the given BST.

**Assume a BST is defined as follows:**

* The left subtree of a node contains only nodes with keys less than or equal to the node's key.
* The right subtree of a node contains only nodes with keys greater than or equal to the node's key.
* Both the left and right subtrees must also be binary search trees.

**For example:**
```
Given BST [1,null,2,2],
   1
    \
     2
    /
   2
return [2].
```
**Note:**

* If a tree has more than one mode, you can return them in any order.

**Follow up:** 

* Could you do that without using any extra space? (Assume that the implicit stack space incurred due to recursion does not count).

## Solutions

### Solution 1
* C++ (26ms) 
```
class Solution {
public:
    int countMode(TreeNode* root, unordered_map<int, int>& count)
    {
        if(root == NULL) return 0;
        count[root->val]++;
        return max(count[root->val], max(countMode(root->left, count), countMode(root->right, count)));
    }
    vector<int> findMode(TreeNode* root) {
        unordered_map<int, int> count;
        int modeSize = countMode(root, count);
        vector<int> res;
        for(pair<int, int> c : count)
            if(c.second == modeSize)
                res.push_back(c.first);
        return res;
    }
};
```

Using map to count the number of each value in the tree. Compare and find the number `modeSize` of the most frequently occurred element. Based on the `modeSize`, find all matched modes in the map.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the number of nodes in the tree `root`.
* **worst-case space complexity:** `O(n)`, where `n` is the number of nodes in the tree `root`.

### Solution 2

* Java
```
class Solution {
    
    private int modeCount;
    private int[] modes;
    private int mostMode;
    private int curCount;
    private int curValue;
    
    public int[] findMode(TreeNode root) {
        inOrder(root);
        modes = new int[modeCount];
        modeCount=0;
        curCount = 0;
        inOrder(root);
        return modes;
    }
    
    private void inOrder(TreeNode root){
        if(root==null) return;
        inOrder(root.left);
        calculateMode(root.val);
        inOrder(root.right);
    }
    
    private void calculateMode(int val){
        if(val != curValue){
            curValue = val;
            curCount=0;
        }
        curCount++;
        if(curCount > mostMode){
            mostMode = curCount;
            modeCount = 1;
        }
        else if(curCount == mostMode){
            if(modes != null)
                modes[modeCount] = curValue;
            modeCount++;
        }
    }
}
```

Do two times of `inOrder` travesal of the tree.

The first time, find the number of the most mode.

The second time, put the modes in the result.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the number of nodes in the tree `root`.
* **worst-case space complexity:** `O(1)`.
