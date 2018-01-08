# LC2. Add Two Numbers

### LeetCode

## Question

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4) 
Output: 7 -> 0 -> 8
```

## Solutions

* C++1
```
ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
    ListNode dummy(0);
    ListNode *pre = &dummy;
    int carry=0;
    while(l1!=NULL || l2!=NULL || carry>0)
    {
        int a = l1==NULL ? 0 : l1->val;
        int b = l2==NULL ? 0 : l2->val;
        int sum = a+b+carry;
        carry = sum/10;
        ListNode *node = new ListNode(sum%10);
        pre->next = node;
        pre = pre->next;
        if(l1!=NULL) l1=l1->next;
        if(l2!=NULL) l2=l2->next;
    }
    return dummy.next;
}
```

* C++2
```
ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
    ListNode head(0), *pre=&head;
    int v1, v2, sum, carry=0;
    while(l1!=NULL || l2!=NULL || carry)
    {
        v1=v2=0;
        if(l1!=NULL)
        {
            v1 = l1->val;
            l1=l1->next;
        }
        if(l2!=NULL)
        {
            v2 = l2->val;
            l2=l2->next;
        }
        sum = v1+v2+carry;
        carry = sum/10;
        pre->next = new ListNode(sum%10);
        pre = pre->next;
    }
    return head.next;
}
```

## Explanation

Add each two nodes from head to end. If one list is shorter than another, assume the rest nodes of the short list are nodes with value `0`.

* **worst-case time complexity:** O(MaxLen(l1, l2))
* **worst-case space complexity:** O(MaxLen(l1, l2))