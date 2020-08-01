# LC95. Unique Binary Search Trees II

### LeetCode

## Question

Given an integer n, generate all structurally unique BST's (binary search trees) that store values 1 ... n.

**Example:**
```
Input: 3

Output:
[
  [1,null,3,2],
  [3,2,null,1],
  [3,1,null,null,2],
  [2,1,3],
  [1,null,2,null,3]
]

Explanation:
The above output corresponds to the 5 unique BST's shown below:

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

**Constraints:**

* 0 <= n <= 8

## Solutions

### Solution 1

* C++
```
vector<TreeNode*> generateBST(int start, int end)
{
    vector<TreeNode*> res;
    if(start > end)
    {
        res.push_back(NULL);
        return res;
    }
    else if(start == end)
    {
        TreeNode* leaf = new TreeNode(start);
        res.push_back(leaf);
        return res;
    }
    for(int i=start; i<=end; ++i)
    {
        vector<TreeNode*> leftNodes = generateBST(start, i-1);
        vector<TreeNode*> rightNodes = generateBST(i+1, end);
        for(auto left : leftNodes)
        {
            for(auto right : rightNodes)
            {
                TreeNode* root = new TreeNode(i);
                root->left = left;
                root->right = right;
                res.push_back(root);
            }
        }
    }
    return res;
}
vector<TreeNode*> generateTrees(int n) {
    if(n<1) return vector<TreeNode*>();
    return generateBST(1, n);
}
```

* Python
```
def generateTrees(self, n: int) -> List[TreeNode]:
    if n == 0:
        return []
    return self.get_trees(1, n)

def get_trees(self, i: int, j: int) -> []:
    if i > j:
        return [None]
    if i == j:
        return [TreeNode(i)]
    
    result = []
    for x in range(i, j + 1):
        left = self.get_trees(i, x - 1)
        right = self.get_trees(x + 1, j)
        
        for l in left:
            for r in right:
                head = TreeNode(x)
                head.left = l
                head.right = r
                result.append(head)
                
    return result
```


