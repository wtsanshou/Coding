# LC21. Merge Two Sorted Lists

### LeetCode

## Question

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

## Solutions

* C++1 (19ms)
```
ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
    if(l1==NULL) return l2;
    if(l2==NULL) return l1;
    if(l1->val < l2->val)
    {
        l1->next = mergeTwoLists(l1->next, l2);
        return l1;
    }
    else
    {
        l2->next = mergeTwoLists(l2->next, l1);
        return l2;
    }
}
```

* C++2 (12ms)
```
ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
    ListNode* min;
    ListNode* max;
    if(l1 && l2)
    {
        min = l1->val <= l2->val? l1:l2;
        max = l2->val >= l1->val? l2:l1;
    }
    else if(l1)
    {
        return l1;
    }
    else 
    {
        return l2;
    }
    ListNode* head = min;
    ListNode* temp;
    while(min && max && min->next)
    {
        if(min->next->val <= max->val)
            min = min->next;
        else
        {
            temp = min->next;
            min->next = max;
            min = max;
            max = temp;
        }
    }
    min->next = max;
    return head;
} 
```

* Java1 (1ms)
```
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode(0);
    ListNode pre = dummy;
    while(l1!=null && l2!=null)
    {
        if(l1.val < l2.val)
        {
            pre.next=l1;
            l1 = l1.next;
        }
        else
        {
            pre.next = l2;
            l2 = l2.next;
        }
        pre = pre.next;
    }
    if(l1!=null)
    {
        pre.next = l1;
    }
    else if(l2!=null)
    {
        pre.next = l2;
    }
    return dummy.next;
}
```

## Explanation

Normally, linear list or tree can be solved by recursion. To save stack memory, recursion can be transformed to iteration.

* **worst-case time complexity:** O(max(Len1, Len2))

**Recursion**

* **worst-case space complexity:** O(max(Len1, Len2))

**Iteration**

* **worst-case space complexity:** O(1)
