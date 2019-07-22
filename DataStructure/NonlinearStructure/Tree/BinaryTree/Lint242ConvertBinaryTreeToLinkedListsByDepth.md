# Lint242. Convert Binary Tree to Linked Lists by Depth

### LintCode

## Question

Given a binary tree, design an algorithm which creates a linked list of all the nodes at each depth (e.g., if you have a tree with depth D, you'll have D linked lists).

**Example 1:**
```
Input: {1,2,3,4}

Output: [1->null,2->3->null,4->null]

Explanation: 
        1
       / \
      2   3
     /
    4
```

**Example 2:**
```
Input: {1,#,2,3}

Output: [1->null,2->null,3->null]

Explanation: 
    1
     \
      2
     /
    3
```

## Solutions

### Solution 1

* Java
```
public List<ListNode> binaryTreeToLists(TreeNode root) {
    List<ListNode> res = new LinkedList<>();
    Deque<TreeNode> queue = new LinkedList<>();
    if (root == null) return res;
    
    queue.add(root);
    
    while (!queue.isEmpty()) {
        ListNode dummy = new ListNode(0);
        ListNode cur = dummy;
        int n = queue.size(); // Important, do not put queue.size() in the loop. the queue is changing.
        for (int i = 0; i < n; i++) {
            TreeNode node = queue.remove();
            cur.next = new ListNode(node.val);
            cur = cur.next;
            if (node.left != null) queue.add(node.left);
            if (node.right != null) queue.add(node.right);
        }
        res.add(dummy.next);
    }
    
    return res;
}
```

When see a question asking for iterate a tree layer by layer, it probably needs to use queue, the idea of BFS. 

**NOTE** you cannot put the `queue.size()` in the loop, because the size of the queue may be changed during the loop.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the number of nodes in the tree `root`.
* **worst-case space complexity:** `O(n)`, where `n` is the number of nodes in the tree `root`.
