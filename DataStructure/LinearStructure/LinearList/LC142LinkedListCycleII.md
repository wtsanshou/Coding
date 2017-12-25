# LC142. Linked List Cycle II

### LeetCode

## Question

Given a linked list, return the node where the cycle begins. If there is no cycle, return null.

**Note:** Do not modify the linked list.

Follow up: Can you solve it without using extra space?

## Solutions

* C++1
```
ListNode *detectCycle(ListNode *head) {
    if(head==NULL) return NULL;
    ListNode *slow=head, *fast=head;
    while(fast!=NULL && fast->next!=NULL)
    {
        slow=slow->next;
        fast=fast->next->next;
        if(slow==fast) break;
    }
    if(fast==NULL || fast->next==NULL) return NULL;
    slow=head;
    while(slow!=fast)
    {
        slow = slow->next;
        fast = fast->next;
    }
    return slow;
}
```

## Explanation

First, find the meet node by <a href="LC141LinkedListCycle.md">LC141. Linked List Cycle</a>.

Suppose the cycle begins is `S` steps from the link head. The cycle is made of `K` nodes. The meet node must be in the cycle `A` steps from the cycle begins node. So the meet node is at `S + A`.

From the meet node, we need to move `n*K + (K-A)` steps to reach the cycle begins. So it is `S + A` + `n*K + (K-A)` = `S + (n+1)*K`.

So, let two pointers, one at the meet node, one at the head node. Let them move one step each time, they will meet at the cycle begins.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)