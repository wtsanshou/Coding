# LC92. Reverse Linked List II

### LeetCode

## Question

Reverse a linked list from position m to n. Do it in-place and in one-pass.

**For example:**

```
Given 1->2->3->4->5->NULL, m = 2 and n = 4,
return 1->4->3->2->5->NULL.
```

**Note:**

Given m, n satisfy the following condition: 1 ≤ m ≤ n ≤ length of list.

## Soltuions

* C++1
```
ListNode* reverseBetween(ListNode* head, int m, int n) {
    ListNode dummy(0);
    dummy.next = head;
    ListNode* cur=head, *pre = &dummy, *nex;
    for(int i=1; i<m; ++i)
    {
        pre = pre->next;
        cur = cur->next;
    }
    for(int i=0; i<n-m; ++i)
    {
        nex = cur->next;
        cur->next = nex->next;
        nex->next = pre->next;
        pre->next = nex;
    }
    return dummy.next;
}
```

* C++2
```
ListNode* reverseBetween(ListNode* head, int m, int n) {
    ListNode* newHead = new ListNode(0);
    newHead->next = head;
    ListNode* pre = newHead;
    for(int i=0; i<m-1; ++i)
    {
        pre = pre->next;
    }
    ListNode* cur = pre->next, *move;
    for(int i=0; i<n-m; ++i)
    {
        move = cur->next;
        cur->next = move->next;
        move->next = pre->next;
        pre->next = move;
    }
    return newHead->next;
}
```

## Explanation

1. Find the previous node of the m<sup>th</sup> node.
2. Reverse from the m<sup>th</sup> node to (m+n)<sup>th</sup> node.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)