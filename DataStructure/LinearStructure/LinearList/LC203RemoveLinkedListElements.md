# LC203. Remove Linked List Elements

### LeetCode

## Question

Remove all elements from a linked list of integers that have value val.

**Example  Given:** 

```
1 --> 2 --> 6 --> 3 --> 4 --> 5 --> 6, 
val = 6  
```

**Return:** 

```
1 --> 2 --> 3 --> 4 --> 5  
```

## Solutions

* C++1 (6ms)
```
ListNode* removeElements(ListNode* head, int val) {
    if(head==NULL) return NULL;
    if(head->val == val)
    {
        ListNode* newHead = head->next;
        head->next = NULL;
        delete head;
        return removeElements(newHead, val);
    }
    head->next = removeElements(head->next, val);
    return head;
}
```

* C++2 (32ms)
```
ListNode* removeElements(ListNode* head, int val) {
    while(head && head->val == val)
    {
        ListNode * d1 = head;
        head = head->next;
        delete d1;
    }
    if(!head) return head;
    ListNode * p = head;
    while(p->next)
    {
        if(p->next->val == val)
        {
            ListNode * d = p->next;
            p->next = p->next->next;
            delete d;
        }
        else
        {
            p = p->next;
        }
    }
    return head;
}
```

* Java1 (2ms)
```
public ListNode removeElements(ListNode head, int val) {
    if(head == null) 
        return head;
    head.next = removeElements(head.next, val);
    return (head.val==val) ? head.next : head;
}
```

* Java2 (2ms)
```
public ListNode removeElements(ListNode head, int val) {
    while(head!=null && head.val==val)
    {
        ListNode del = head;
        head = head.next;
        del = null;
    }
    if(head == null) 
        return head;
    head.next = removeElements(head.next, val);
    return head;
}
```

* Java2 (2ms)
```
public ListNode removeElements(ListNode head, int val) {
    while(head!=null && head.val==val)
    {
        ListNode del = head;
        head = head.next;
        del = null;
    }
    if(head == null) 
        return head;
    ListNode cur = head;
    while(cur.next!=null)
    {
        if(cur.next.val==val)
        {
            ListNode del1 = cur.next;
            cur.next = del1.next;
            del1 = null;
        }
        else
            cur = cur.next;
    }
    return head;
}
```

## Explanation

Java1 is the most concise solution. The idea is to recurse into the end of the list, only return nodes whose value is not equal to the target value.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)