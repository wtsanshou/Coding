# LC237. Delete Node in a Linked List

### LeetCode

## Question

Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.

Supposed the linked list is `1 -> 2 -> 3 -> 4` and you are given the third node with value 3, the linked list should become `1 -> 2 -> 4` after calling your function.

## Solutions

* C++1 (20ms)
```
void deleteNode(ListNode* node) {
    ListNode* p = node->next;
    *node = *p;
    delete p;
}
```

* C++2 (19ms)
```
void deleteNode(ListNode* node) {
    ListNode* del = node->next;
    node->val = del->val;
    node->next = del->next;
    delete del;
}
```

* Java1 (1ms)
```
public void deleteNode(ListNode node) {
    node.val = node.next.val;
    node.next = node.next.next;
}
```

## Explanation

1. Replace the current node's value by the next's next's value. 
2. Delete the next node.

* **worst-case time complexity:** O(1)
* **worst-case space complexity:** O(1)