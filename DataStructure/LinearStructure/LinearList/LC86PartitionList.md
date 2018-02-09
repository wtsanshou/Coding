# LC86. Partition List

### LeetCode

## Question

Given a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

You should preserve the original relative order of the nodes in each of the two partitions.

For example, 
```
Given: 1->4->3->2->5->2 and x = 3

return: 1->2->2->4->3->5.
```

## Solutions

* C++1
```
ListNode* partition(ListNode* head, int x) {
    ListNode left(0), right(0);
    ListNode *L=&left, *R=&right;
    while(head != NULL)
    {
        if(head->val < x) 
        {
            L->next = head;
            L = L->next;
        }
        else
        {
            R->next = head;
            R = R->next;
        }
        head = head->next;
    }
    L->next = right.next;
    R->next = NULL;
    return left.next;
}
```

## Explanation

Create two lists for the two partitions, and then link them together

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)