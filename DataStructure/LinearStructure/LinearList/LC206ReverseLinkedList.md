# LC206. Reverse Linked List

### LeetCode

## Question

Reverse a singly linked list.

A linked list can be reversed either iteratively or recursively. Could you implement both?

## Solutions

* C++1 (8ms)
```
ListNode* reverseList(ListNode* head) {
    ListNode* p1 = NULL;
    ListNode * Next;
    while(head)
    {
        Next = head->next;
        head->next = p1;
        p1 = head;
        head = Next;
    }
    return p1;
}
```

* C++2 (12ms)
```
ListNode* reverseList(ListNode* head) {
    if(!head || !head->next)
        return head;
    ListNode* p1 = reverseList(head->next);
    head->next->next = head;
    head->next = NULL;
    return p1;
}
```

## Explanation

**Iteration**

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)

**Recursion**

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(n)
