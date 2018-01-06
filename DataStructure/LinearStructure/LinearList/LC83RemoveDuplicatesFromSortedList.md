# LC83. Remove Duplicates from Sorted List

### LeetCode

## Question

Given a sorted linked list, delete all duplicates such that each element appear only once.

**For example:**

```
Given 1->1->2, return 1->2.
Given 1->1->2->3->3, return 1->2->3.
```

## Solution

* C++1 (9ms)
```
ListNode* deleteDuplicates(ListNode* head) {
    if(head == NULL || head->next==NULL) return head;
    ListNode* p = head;
    while(p->next != NULL)
    {
        if(p->val == p->next->val)
        {
            ListNode *del = p->next;
            p->next = del->next;
            delete del;
        }
        else if(p->next != NULL) p = p->next;
    }
    return head;
}
```

## Explanation

If next node's value equals the current node's value, delete the next node.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)