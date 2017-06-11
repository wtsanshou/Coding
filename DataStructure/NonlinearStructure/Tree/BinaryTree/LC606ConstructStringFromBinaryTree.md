# Construct String from Binary Tree

### LeetCode

## Question

You need to construct a string consists of parenthesis and integers from a binary tree with the preorder traversing way.

The null node needs to be represented by empty parenthesis pair "()". And you need to omit all the empty parenthesis pairs that don't affect the one-to-one mapping relationship between the string and the original binary tree.

**Example 1:**

**Input:** 

Binary tree: [1,2,3,4]
```
       1
     /   \
    2     3
   /    
  4     
```

**Output:** 
```
"1(2(4))(3)"
```

**Explanation:** 

Originallay it needs to be "1(2(4)())(3()())", but you need to omit all the unnecessary empty parenthesis pairs. And it will be "1(2(4))(3)".

**Example 2:**

**Input:**

Binary tree: [1,2,3,null,4]
```
       1
     /   \
    2     3
     \  
      4 
```

**Output:**
```
 "1(2()(4))(3)"
```

**Explanation:** 

Almost the same as the first example, except we can't omit the first parenthesis pair to break the one-to-one mapping relationship between the input and the output.

## Solution

* C++1
```
string tree2str(TreeNode* t) {
        if(t==NULL) return "";
        string res = to_string(t->val);
        if(t->left==NULL && t->right==NULL)
            return res;
        else if(t->left!=NULL && t->right==NULL)
            return res + "(" + tree2str(t->left) + ")";
        return res + "(" + tree2str(t->left) + ")" + "(" + tree2str(t->right) + ")";
    }
```

## Explanation

For tree question, normally check:

1. root == NULL
2. root->left==NULL && root->right==NULL
3. root->left==NULL || root->right==NULL
4. root->left!=NULL && root->right!=NULL

In this question:

1. if `root==NULL`,                            return `empty string`
2. if `root->left==NULL && root->right==NULL`, return `root value`
3. if `root->left!=NULL && root->right==NULL`, return `root value + (left tree)`
4. if `root->left==NULL && root->right!=NULL`, return `root value + () + (right tree)`
5. if `root->left!=NULL && root->right!=NULL`, return `root value + (left tree) + (right tree)`

Here, step 4 and step 5 could be combined together.
