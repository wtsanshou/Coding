# LC160. Intersection of Two Linked Lists

### LeetCode

## Question

Write a program to find the node at which the intersection of two singly linked lists begins.

For example, the following two linked lists:

```
A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3
```

begin to intersect at node c1.

**Notes:**

* If the two linked lists have no intersection at all, return null.
* The linked lists must retain their original structure after the function returns.
* You may assume there are no cycles anywhere in the entire linked structure.
* Your code should preferably run in O(n) time and use only O(1) memory.

## Solutions

* C++1 (52ms)
```
ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
    ListNode* lA = headA;
    ListNode* lB = headB;
    while(lA!=NULL || lB!=NULL)
    {
        if(lA == lB) return lA;
        lA = (lA != NULL) ? lA->next : headB;
        lB = (lB != NULL) ? lB->next : headA;
    }
    return NULL;
}
```

* C++2 (60ms)
```
ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
    ListNode *l1 = headA, *l2 = headB;
    while(l1!=l2)
    {
        l1 = l1? l1->next:headB;
        l2 = l2? l2->next:headA;
    }
    return l1;
}
```

* Java1 (2ms)
```
public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
    ListNode la = headA, lb=headB;
    while(la!=lb)
    {
        if(la==null) la=headB;
        else la = la.next;
        
        if(lb==null) lb = headA;
        else lb = lb.next;
    }
    return la;
}
```

## Explanation

Distance(a1, c3) + Distance(b1, b3) == Distance(b1, c3) + Distance(a1, a2)

* **worst-case time complexity:** O(m+n)
* **worst-case space complexity:** O(1)