# LC24. Swap Nodes in Pairs

### LeetCode

## Question

Given a linked list, swap every two adjacent nodes and return its head.
For example, Given `1->2->3->4`, you should return the list as `2->1->4->3`.
Your algorithm should use only constant space. You may not modify the values in the list, only nodes itself can be changed.

## Solutions

* C++1
```
ListNode* swapPairs(ListNode* head) {
    if(head==NULL || head->next==NULL) return head;
    ListNode* newHead = head->next;
    head->next = newHead->next;
    newHead->next = head;
    head->next = swapPairs(head->next);
    return newHead;
}
```

* C++2
```
ListNode* swapPairs(ListNode* head) {
    if(!head || !head->next) return head;
    ListNode* p = head->next;
    head->next = swapPairs(p->next);
    p->next = head;
    return p;
}
```

* C++3
```
ListNode* swapPairs(ListNode* head) {
    ListNode **pp = &head, *a, *b;
    while ((a = *pp) && (b = a->next)) {
        a->next = b->next;
        b->next = a;
        *pp = b;
        pp = &(a->next);
    }
    return head;
}
```

* Java1
```
public ListNode swapPairs(ListNode head) {
    if(head==null || head.next==null) return head;
    ListNode dummy = new ListNode(0);
    ListNode pre = dummy;
    while(head!=null && head.next!=null)
    {
        pre.next = head.next;
        head.next = pre.next.next;
        pre.next.next = head;
        pre = head;
        head = head.next;
    }
    return dummy.next;
}
```

## Explanation

Recursive and iteration solutions, swap a pair and move to next pair.

* **worst-case time complexity:** O(n)

**Iteration**

* **worst-case space complexity:** O(1)

**Recursive**

* **worst-case space complexity:** O(n)
