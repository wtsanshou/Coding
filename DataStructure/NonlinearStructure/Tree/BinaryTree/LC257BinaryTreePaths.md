# LC257. Binary Tree Paths

### LeetCode

## Question

Given a binary tree, return all root-to-leaf paths.
For example, given the following binary tree:

```
   1
 /   \
2     3
 \
  5
```

All root-to-leaf paths are:

`["1->2->5", "1->3"]`

## Solutions

* C++1 (9ms) 
```
void TraceTreePaths(vector<string>&res, string aPath, TreeNode* root)
{
    if(root->left==NULL && root->right==NULL) res.push_back(aPath);
    else
    {
        if(root->left!=NULL) TraceTreePaths(res, aPath+"->"+to_string(root->left->val), root->left);
        if(root->right!=NULL) TraceTreePaths(res, aPath+"->"+to_string(root->right->val), root->right);
    }
}

vector<string> binaryTreePaths(TreeNode* root) {
    vector<string> res;
    if(root==NULL) return res;
    TraceTreePaths(res, to_string(root->val), root);
    return res;
}
```

* C++2 (4ms) 
```
vector<string> binaryTreePaths(TreeNode* root) {
    vector<string> res;
    if (root == NULL) return res;
    stack<TreeNode*> s;
    stack<string> pathStack;
    s.push(root);
    pathStack.push(to_string(root->val));

    while (!s.empty()) {
        TreeNode * curNode = s.top(); s.pop();
        string tmpPath = pathStack.top(); pathStack.pop();

        if (curNode->left == NULL && curNode->right == NULL) {
            res.push_back(tmpPath); continue;
        }

        if (curNode->left != NULL) {
            s.push(curNode->left);
            pathStack.push(tmpPath + "->" + to_string(curNode->left->val));
        }

        if (curNode->right != NULL) {
            s.push(curNode->right);
            pathStack.push(tmpPath + "->" + to_string(curNode->right->val));
        }
    }
    return res;
}
```

* Java1 (2ms) 
```
private List<String> res;
public List<String> binaryTreePaths(TreeNode root) {
    res = new ArrayList<String>();
    if(root!=null) inputPath(root, "");
    return res;
}

public void inputPath(TreeNode root, String arow) {
    if(root.left==null && root.right==null)
        res.add(arow+root.val);
    if(root.left!=null) 
        inputPath(root.left, arow+root.val+"->");
    if(root.right!=null) 
        inputPath(root.right, arow+root.val+"->");
}
```

## Explanation

Normally, tree can be sovled by recursive algorithm. 

Recurse down to each leaf, start to put node value into result.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(h)