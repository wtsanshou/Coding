# LC328. Odd Even Linked List

### LeetCode

## Question

Given a singly linked list, group all odd nodes together followed by the even nodes. Please note here we are talking about the node number and not the value in the nodes.

You should try to do it in place. The program should run in O(1) space complexity and O(nodes) time complexity.

**Example:**

```
Given 1->2->3->4->5->NULL, 
return 1->3->5->2->4->NULL.
```

**Notea:**

The relative order inside both the even and odd groups should remain as it was in the input.  The first node is considered odd, the second node even and so on ...

## Solutions

* C++1 (19ms) 
```
ListNode* oddEvenList(ListNode* head) {
    if(head==NULL) return head;
    ListNode* odd = head;
    ListNode* evenHead = head->next;
    ListNode* even = evenHead;
    while(even != NULL && even->next!=NULL)
    {
        odd->next = even->next;
        even->next = odd->next->next;
        odd = odd->next;
        even = even->next;
    }
    odd->next = evenHead;
    return head;
}
```

* Java1 (1ms)
```
public ListNode oddEvenList(ListNode head) {
    if(head == null) return null;
    ListNode odd = head, even = head.next;
    ListNode evenHead = even;
    while(even!=null && even.next!=null)
    {
        odd.next = even.next;
        even.next = even.next.next;
        odd = odd.next;
        even = even.next;
    }
    odd.next = evenHead;
    return head;
}
```

## Explanation

1. Link odd nodes `odd-link`, link even nodes `even-link`.
2. Link `odd-link` and `even-link` together.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)
