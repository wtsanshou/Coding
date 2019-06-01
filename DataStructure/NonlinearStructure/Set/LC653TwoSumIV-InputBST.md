# LC653. Two Sum IV - Input is a BST

### LeetCode

## Question

Given a Binary Search Tree and a target number, return true if there exist two elements in the BST such that their sum is equal to the given target.

**Example 1:**

**Input:** 
```
    5
   / \
  3   6
 / \   \
2   4   7
```
Target = 9

Output: True

**Example 2:**

**Input:** 
```
    5
   / \
  3   6
 / \   \
2   4   7
```
Target = 28

Output: False

## Solutions

### Solution 1

* C++
```
bool findTargetIn(unordered_set<int>& set, TreeNode* root, int k)
    {
        if(root == NULL) return false;
        if(set.find(k - root->val) != set.end()) return true;
        set.insert(root->val);
        return findTargetIn(set, root->left, k) || findTargetIn(set, root->right, k);
    }
    
    bool findTarget(TreeNode* root, int k) {
        unordered_set<int> set;
        return findTargetIn(set, root, k);
}
```

* Java
```public boolean findTarget(TreeNode root, int k) {
        Set<Integer> set = new HashSet<>();
        return findTargetIn(set, root, k);
    }
    
    private boolean findTargetIn(Set<Integer> set, TreeNode root, int k){
        if(root == null) return false;
        if(set.contains(k - root.val)) return true;
        set.add(root.val);
        return findTargetIn(set, root.left, k) || findTargetIn(set, root.right, k);
    }
```

## Explanation

Using a set to save up layers values could avoid judge if duplicate values in the BST.

Another way is to convert the BST to a sorted array, then see the question <a>LC167. Two Sum II - Input array is sorted</a>. But this way is not the purpose of this question.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the number of nodes in the tree `root`.
* **worst-case space complexity:** `O(n)`, where `n` is the number of nodes in the tree `root`.

### Solution 2

Instead of using set, we can search the `k - root.val` in the BST.

**Complexity:**

* **worst-case time complexity:** `O(n * log(n))`, where `n` is the number of nodes in the tree `root`.
* **worst-case space complexity:** `O(1)`
