# LC117. Populating Next Right Pointers in Each Node II

### LeetCode

## Question

Follow up for problem "Populating Next Right Pointers in Each Node".

What if the given tree could be any binary tree? Would your previous solution still work?

**Note:**

* You may only use constant extra space.

For example, Given the following binary tree,

```
         1
       /  \
      2    3
     / \    \
    4   5    7
```

After calling your function, the tree should look like:
```
         1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \    \
    4-> 5 -> 7 -> NULL
```

## Solutions

* C++1
```
void connect(TreeLinkNode *root) {
    if(root==NULL) return;
    TreeLinkNode dummy(0);
    TreeLinkNode *cur=root, *pre = &dummy;
    while(cur)
    {
        for(pre=&dummy; cur; cur=cur->next)
        {
            if(cur->left != NULL)
            {
                pre->next = cur->left;
                pre = pre->next;
            }
            if(cur->right != NULL)
            {
                pre->next = cur->right;
                pre = pre->next;
            }
        }
        cur = dummy.next; //dummy point to the next first left child
        dummy.next = NULL;
    }
}
```

## Explanation

Travel the tree layer by layer, connect the current layer's children.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)