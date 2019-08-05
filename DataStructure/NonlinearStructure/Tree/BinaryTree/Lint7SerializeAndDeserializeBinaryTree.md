# Lint7. Serialize and Deserialize Binary Tree

### LintCode

## Question

Design an algorithm and write code to serialize and deserialize a binary tree. Writing the tree to a file is called 'serialization' and reading back from the file to reconstruct the exact same binary tree is 'deserialization'.

**Example 1:**
```
Input：
{3,9,20,#,#,15,7}

Output：
{3,9,20,#,#,15,7}

Explanation：
Binary tree {3,9,20,#,#,15,7},  denote the following structure:
	  3
	 / \
	9  20
	  /  \
	 15   7
it will be serialized {3,9,20,#,#,15,7}
```

**Example 2:**
```
Input：
{1,2,3}

Output：
{1,2,3}

Explanation：
Binary tree {1,2,3},  denote the following structure:
   1
  / \
 2   3
it will be serialized {1,2,3}
```

Our data serialization use BFS traversal. This is just for when you got Wrong Answer and want to debug the input.

You can use other method to do serializaiton and deserialization.

**Notice**

* There is no limit of how you deserialize or serialize a binary tree, LintCode will take your output of serialize as the input of deserialize, it won't check the result of serialize.

## Solutions

### Solution 1

* Java
```
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */


public class Solution {
    /**
     * This method will be invoked first, you should design your own algorithm 
     * to serialize a binary tree which denote by a root node to a string which
     * can be easily deserialized by your own "deserialize" method later.
     */
     
    private final String NULL_NODE = "#";
    private final String SPLITER = ",";
     
    public String serialize(TreeNode root) {
        // write your code here
        return serializeTree(root, new StringBuilder()).toString();
    }
    
    private StringBuilder serializeTree(TreeNode root, StringBuilder sb) {
        if (root == null) {
            sb.append(NULL_NODE).append(SPLITER);
            return sb;
        }
        
        sb.append(root.val).append(SPLITER);
        serializeTree(root.left, sb);
        serializeTree(root.right, sb);
        return sb;
    }

    /**
     * This method will be invoked second, the argument data is what exactly
     * you serialized at method "serialize", that means the data is not given by
     * system, it's given by your own serialize method. So the format of data is
     * designed by yourself, and deserialize it here as you serialize it in 
     * "serialize" method.
     */
    public TreeNode deserialize(String data) {
        // write your code here
        Queue<String> queue = new LinkedList<>();
        String[] values = data.split(SPLITER);
        queue.addAll(Arrays.asList(values));
        return deserializeTree(queue);
    }
    
    private TreeNode deserializeTree(Queue<String> queue) {
        String value = queue.remove();
        if (NULL_NODE.equals(value))
            return null;
        TreeNode root = new TreeNode(Integer.valueOf(value));
        root.left = deserializeTree(queue);
        root.right = deserializeTree(queue);
        return root;
    }
}
```

Using preorder traversal to serialize and deserialize the tree.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the number of nodes in the tree.
* **worst-case space complexity:** `O(n)`, where `n` is the number of nodes in the tree.