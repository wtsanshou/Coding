# LC637. Average of Levels in Binary Tree

### LeetCode

## Question

Given a non-empty binary tree, return the average value of the nodes on each level in the form of an array.

**Example 1:**

**Input:**
```
    3
   / \
  9  20
    /  \
   15   7
```

**Output:** [3, 14.5, 11]

**Explanation:**

The average value of nodes on level 0 is 3,  on level 1 is 14.5, and on level 2 is 11. Hence return [3, 14.5, 11].

Note:

1.  The range of node's value is in the range of 32-bit signed integer.

## Solutions

* C++1

```
vector<double> averageOfLevels(TreeNode* root) {
        vector<double> res;
        if(root==NULL) return res;
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty())
        {
            int size = q.size();
            double ave = 0;
            for(int i=0; i<size; ++i)
            {
                TreeNode* node = q.front();
                q.pop();
                ave += node->val;
                if(node->left  != NULL) q.push(node->left);
                if(node->right != NULL) q.push(node->right);
            }
            res.push_back(ave/size);
        }
        return res;
}
```

* Java1

```
public List<Double> averageOfLevels(TreeNode root) {
        List<Double> res = new LinkedList<>();
        if(root == null) return res;
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);
        while(!q.isEmpty()){
            int size = q.size();
            double ave = 0.0;
            for(int i=0; i<size; ++i){
                TreeNode node = q.remove();
                ave += node.val;
                if(node.left  != null) q.add(node.left);
                if(node.right != null) q.add(node.right);
            }
            res.add(ave/size);
        }
        return res;
    }
```

## Explanation

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(n)