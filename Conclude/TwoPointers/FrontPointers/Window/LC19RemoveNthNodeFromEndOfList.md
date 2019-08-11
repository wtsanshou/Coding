# LC19. Remove Nth Node From End of List

### LeetCode

## Question

Given a linked list, remove the nth node from the end of list and return its head.

**For example,**

Given linked list: `1->2->3->4->5`, and n = 2.

After removing the second node from the end, the linked list becomes `1->2->3->5`.

**Note:** Given n will always be valid. Try to do this in one pass.

## Solutions

### Solution 1

* C++1
```
ListNode* removeNthFromEnd(ListNode* head, int n) {
    ListNode dummy(0);
    dummy.next = head;
    ListNode* preDel = &dummy, *fast=head;
    for(int i=0; i<n && fast; ++i)
        fast = fast->next;
    while(fast!=NULL)
    {
        preDel = preDel->next;
        fast = fast->next;
    }
    if(preDel->next!=NULL)
    {
        ListNode* del = preDel->next;
        preDel->next = del->next;
        del->next = NULL;
        delete del;
    }
    return dummy.next;
}
```

* C++2
```
ListNode* removeNthFromEnd(ListNode* head, int n) {
    ListNode* p1 = head, *p2 = head;
    for(int i=0; i<n; i++)
        p2 = p2->next;
    if(p2==NULL)
    {
        p1=head->next;
        head->next = NULL;
        return p1;
    }
    while(p2->next)
    {
        p1 = p1->next;
        p2 = p2->next;
    }
    p2 = p1->next;
    p1->next = p2->next;
    p2->next = NULL;
    return head;
}
```

* C++3
```
ListNode* removeNthFromEnd(ListNode* head, int n) {
    ListNode** p1 = &head, *p2 = head;
    for(int i=0; i<n-1; i++)
        p2 = p2->next;
    while(p2->next)
    {
        p1 = &((*p1)->next);
        p2 = p2->next;
    }
    *p1 = (*p1)->next;
    return head;
}
```

## Explanation

Using two pointers `p1` and `p2`. `p1` points to a dummy node whose next node is the head of the list. 'p2' points to the head of the list. Let `p2` move `n` step first. Then let `p1` and `p2` move one step per time. when `p2` reaches the end of the list, `p1` points to the previous node of the target node. Then delete it.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)

### Solution 2

* Java
```
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        int len = 0;
        ListNode slow = dummy;
        ListNode faster = head;
        
        for (; slow.next != null; slow = slow.next) {
            while (faster != null && len < n) {
                faster = faster.next;
                len++;
            }
            
            if (faster == null)
                break;
            
            len--;
        }
        
        if (slow.next != null) {
            ListNode temp = slow.next;
            slow.next = temp.next;
            temp = null;
        }
        
        return dummy.next;
    }
}
```

1. Two loops
2. No need to put `faster` back.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the number of nodes in the list `head`.
* **worst-case space complexity:** `O(1)`.
