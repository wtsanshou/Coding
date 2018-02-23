# LC61. Rotate List

### LeetCode

## Question

Given a list, rotate the list to the right by k places, where k is non-negative.

**For example:**
```
Given 1->2->3->4->5->NULL and k = 2,
return 4->5->1->2->3->NULL.
```

## Solutions

* C++1
```
ListNode* rotateRight(ListNode* head, int k) {
    if(head==NULL) return head;
    int len = 0;
    ListNode* cur = head;
    while(cur!=NULL)
    {
        len++;
        cur=cur->next;
    }
    k = k%len;
    if(k==0) return head; //corner cases: len=1, k%len==0
    ListNode* slow=head, *fast=head;
    for(int i=0; i<k; ++i)
        fast = fast->next;
    while(fast->next!=NULL)
    {
        slow = slow->next;
        fast = fast->next;
    }
    ListNode* newHead = slow->next;
    slow->next = NULL;
    fast->next=head;
    return newHead;
}
```

* C++2
```
ListNode* rotateRight(ListNode* head, int k) {
    if(head==NULL || k==0) return head;
    ListNode *first = head, *tail = head;
    int len = 1;
    while(first->next!=NULL)
    {
        len++;
        first = first->next;
    }
    k %= len;
    if(k==0) return head;
    for(int i=1; i<len-k; ++i) tail = tail->next;
    
    first->next = head;
    head = tail->next;
    tail->next = NULL;
    
    return head;
}
```

## Explanation

1. Count the length `len` of the list.
2. `k %= len`.
3. Cut the list into two parts.
4. Change the front and back positions of the two parts.

**Note:** `k` might be larger than `len`.

* **worst-case time complexity:** O(N)
* **worst-case space complexity:** O(1)