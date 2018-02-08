# LC147. Insertion Sort List

### LeetCode

## Question

Sort a linked list using insertion sort.

## Solutions

* C++1
```
ListNode* insertionSortList(ListNode* head) {
    ListNode dummy(0);
    //dummy->next = head; //if has this connection, will create a circle, will be ETL
    ListNode* cur=head, *pre = &dummy;
    while(cur != NULL)
    {
        ListNode* temp = cur->next;
        if(pre->next==NULL || pre->next->val > cur->val) pre = &dummy;
        while(pre->next!=NULL && pre->next->val < cur->val)
            pre = pre->next;
        cur->next = pre->next;
        pre->next = cur;
        cur = temp;
    }
    return dummy.next;
}
```

* C++2
```
ListNode* insertionSortList(ListNode* head) {
    if(head==NULL || head->next==NULL) return head; 
    ListNode* newHead = new ListNode(0);
    ListNode* cur = head, *pre = newHead, *move=NULL;
    while(cur!=NULL)
    {
        move = cur->next;
        if(!pre || !pre->next || pre->next->val >= cur->val) pre = newHead;
        while(pre->next!=NULL && pre->next->val<cur->val)
            pre = pre->next;
        cur->next = pre->next;
        pre->next = cur;
       // pre = newHead;
        cur = move;
    }
    return newHead->next;
}
```

* C++3 (traditional way, very slow)
```
ListNode* insertionSortList(ListNode* head) {
    if(head==NULL || head->next==NULL) return head; 
    ListNode* newHead = new ListNode(0);
    ListNode* cur = head, *pre = newHead, *move=NULL;
    while(cur!=NULL)
    {
        move = cur->next;
        while(pre->next!=NULL && pre->next->val<cur->val)
            pre = pre->next;
        cur->next = pre->next;
        pre->next = cur;
        pre = newHead;
        cur = move;
    }
    return newHead->next;
}
```

## Explanation

Keep a pointer at the beginning of the list. 

Check each node, find a place from beginning and insert the node.

* **worst-case time complexity:** O(n<sup>2</sup>)
* **worst-case space complexity:** O(1)