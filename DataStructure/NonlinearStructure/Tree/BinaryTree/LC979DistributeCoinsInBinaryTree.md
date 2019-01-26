# LC979. Distribute Coins in Binary Tree

### LeetCode

## Question

Given the root of a binary tree with N nodes, each node in the tree has node.val coins, and there are N coins total.

In one move, we may choose two adjacent nodes and move one coin from one node to another.  (The move may be from parent to child, or from child to parent.)

Return the number of moves required to make every node have exactly one coin.

**Example 1:**

![LC979. Distribute Coins in Binary Tree](Images/LC979DistributeCoinsInBinaryTree1.png)
```
Input: [3,0,0]
Output: 2
Explanation: From the root of the tree, we move one coin to its left child, and one coin to its right child.
```

**Example 2:**

![LC979. Distribute Coins in Binary Tree](Images/LC979DistributeCoinsInBinaryTree2.png)
```
Input: [0,3,0]
Output: 3
Explanation: From the left child of the root, we move two coins to the root [taking two moves].  Then, we move one coin from the root of the tree to the right child.
```

**Example 3:**

![LC979. Distribute Coins in Binary Tree](Images/LC979DistributeCoinsInBinaryTree3.png)
```
Input: [1,0,2]
Output: 2
```

**Example 4:**

![LC979. Distribute Coins in Binary Tree](Images/LC979DistributeCoinsInBinaryTree4.png)
```
Input: [1,0,0,null,3]
Output: 4
``` 

**Note:**

* 1<= N <= 100
* 0 <= node.val <= N

## Solutions
* Scala1
```
def distributeCoins(root: TreeNode): Int = {
    if(root==null) return 0
    else if(root.left==null && root.right==null){
        root.value -= 1
        return root.value
    } 
    var left = 0
    var right = 0
    if(root.left==null){
        right = distributeCoins(root.right)
        root.value += (root.right.value - 1)
    }
    else if(root.right == null){
        left = distributeCoins(root.left)
        root.value += (root.left.value - 1)
    }  
    else{
        left = distributeCoins(root.left)
        right = distributeCoins(root.right)
        root.value += (root.left.value + root.right.value - 1)
    }
    Math.abs(root.value) + Math.abs(left) + Math.abs(right) 
}
```

## Explanation

The idea is to use the nodes to save the possible number of coins which need to move:

* positive number: number of coins which need to move out
* negitive number: number of coins which need to move in

Finally, return the number of coins which need to move in the current node + the number of coins which has moved in the left tree + the number of coins which has moved in the right tree.

* **worst-case time complexity:** `O(log(n))`, where `n` is the number of the nodes in the tree.
* **worst-case space complexity:** `O(log(n))`, where `n` is the number of the nodes in the tree.

