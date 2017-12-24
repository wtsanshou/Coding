# LC141. Linked List Cycle

### LeetCode

## Question

Given a linked list, determine if it has a cycle in it.
Follow up: Can you solve it without using extra space?

## Solutions

* C++1 (9ms) 
```
bool hasCycle(ListNode *head) {
    ListNode* slow = head;
    ListNode* fast = head;
    while(fast!=NULL && fast->next!=NULL)
    {
        slow = slow->next;
        fast = fast->next->next;
        if(slow == fast) return true;
    }
    return false;
}
```

* C++2 (14ms) 
```
bool hasCycle(ListNode *head) {
    if(!head) return false;
    if(!head->next) return false;
    ListNode*p1 = head;
    ListNode*p2 = head->next->next;
    while(p2 && p2->next)
    {
        if(p1==p2)
            return true;
        p1=p1->next;
        p2=p2->next->next;
    }
    return false;
}
```

* Java1 (1ms) 
```
public boolean hasCycle(ListNode head) {
    ListNode slow=head, fast=head;
    while(fast!=null && fast.next!=null)
    {
        slow=slow.next;
        fast=fast.next.next;
        if(slow==fast) return true;
    }
    return false;
}
```

## Explanation

Two pointers, one pointer move one step each time, another pointer move two steps each time. If the list is cycle, they must meet at a node.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)