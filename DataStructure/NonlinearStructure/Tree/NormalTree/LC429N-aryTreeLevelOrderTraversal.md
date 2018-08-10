# LC429. N-ary Tree Level Order Traversal

### LeetCode

## Question

Given an n-ary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example, given a 3-ary tree:
 
![LC429. N-ary Tree Level Order Traversal](Images/LC429N-aryTreeLevelOrderTraversal.png)
 
We should return its level order traversal:
```
[
     [1],
     [3,2,4],
     [5,6]
]
```

**Note:**

* The depth of the tree is at most 1000.
* The total number of nodes is at most 5000.

## Solutions
* Java1
```
public List<List<Integer>> levelOrder(Node root) {
    List<List<Integer>> res = new LinkedList();
    List<Node> queue = new LinkedList();
    queue.add(root);
    queue.add(null);
    while(!queue.isEmpty()){
        Node node = queue.remove(0);
        if(node == null) break;
        List<Integer> row = new LinkedList();
        while(node != null){
            row.add(node.val);
            for(Node n : node.children)
                queue.add(n);
            node = queue.remove(0);
        }
        res.add(row);
        queue.add(null);
    }
    return res;
}
```

# Explanation

Using queue to get layer by layer.

* **worst-case time complexity:** O(log(n)), where n is the number of the nodes in the tree.
* **worst-case space complexity:** O(n), where n is the number of the nodes in the tree.
