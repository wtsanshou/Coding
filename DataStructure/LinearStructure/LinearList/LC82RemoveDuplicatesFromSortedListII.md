# LC82. Remove Duplicates from Sorted List II

### LeetCode

## Question

Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

**For example**

```
Given 1->2->3->3->4->4->5, return 1->2->5.
Given 1->1->1->2->3, return 2->3.
```

## Solutions

* C++1
```
ListNode* deleteDuplicates(ListNode* head) {
    if(head == NULL || head->next==NULL) return head;
    if(head->val == head->next->val)
    {
        ListNode* move = head;
        while(move->next!=NULL && move->val == move->next->val)
            move = move->next;
        return deleteDuplicates(move->next);
    }
    else
        head->next = deleteDuplicates(head->next);
    return head;
}
```

## Explanation

1. If found duplicated nodes, move to the last of the duplicated node, and recurse the next node.
2. If the current node is not duplicated, keep it for result.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)