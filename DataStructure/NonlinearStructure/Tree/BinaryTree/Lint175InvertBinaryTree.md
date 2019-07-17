# Lint175. Invert Binary Tree

### LintCode

## Question

Invert a binary tree.Left and right subtrees exchange.

**Example 1:**
```
Input: {1,3,#}

Output: {1,#,3}

Explanation:
	  1    1
	 /  =>  \
	3        3
```

**Example 2:**
```
Input: {1,2,3,#,#,4}

Output: {1,3,2,#,4}

Explanation: 
      1         1
     / \       / \
    2   3  => 3   2
       /       \
      4         4
```

**Challenge**

Do it in recursion is acceptable, can you do it without recursion?

## Solutions

### Solution 1

* Java
```
public class Solution {
    /**
     * @param root: a TreeNode, the root of the binary tree
     * @return: nothing
     */
    public void invertBinaryTree(TreeNode root) {
        invert(root);
    }
    
    private TreeNode invert(TreeNode root) {
        if (root == null) 
            return root;
        TreeNode left = root.left;
        root.left = invert(root.right);
        root.right = invert(left);
        return root;
    }
}
```

**Note** this question ask for return nothing. So I have to create a private method to do recursive. The key is just a swap.

Recursion is bottom up solution.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the number of nodes in the tree `root`.
* **worst-case space complexity:** `O(log(n))`, where `n` is the number of nodes in the tree `root`.

### Solution 2

* Java
```
public void invertBinaryTree(TreeNode root) {
    if (root == null) return;
    Deque<TreeNode> stack = new LinkedList<>();
    stack.addFirst(root);
    while (stack.isEmpty() == false) {
        TreeNode cur = stack.removeFirst();
        TreeNode left = cur.left;
        cur.left = cur.right;
        cur.right = left;
        if (cur.left != null) stack.addFirst(cur.left);
        if (cur.right != null) stack.addFirst(cur.right);
    }
}
```

Normally, the iteration solution of the recursion problem is to use stack. 

iteration is top down solution.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the number of nodes in the tree `root`.
* **worst-case space complexity:** `O(n)`, where `n` is the number of nodes in the tree `root`.

