# Lint19. Insert Node in Sorted Linked List

Insert a node in a sorted linked list.

**Example 1:**
```
Input: head = 1->4->6->8->null, val = 5
Output: 1->4->5->6->8->null
```

**Example 2:**
```
Input: head = 1->null, val = 2
Output: 1->2->null
```

## Solutions

## Solution 1

* Java
```
public ListNode insertNode(ListNode head, int val) {
    ListNode keyNode = new ListNode(val);
    if(head == null) return keyNode;
    ListNode newHead = head;
    if(val<=head.val) {
        keyNode.next = head;
        return keyNode;
    }
    
    for(; head!=null; head=head.next){
        if(head.next!=null && head.val<=val && val<=head.next.val){
            keyNode.next = head.next;
            head.next = keyNode;
            return newHead;
        }
        else if(head.next==null){
            head.next = keyNode;
            return newHead;
        }
    }
    
    return newHead;
}
```

**Corner cases**

1. `head` is null.
2. The `val` is equal or smaller than the first value of the list.
3. The `val` is equal or larger than the last value of the list.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the `arr`, `k` is the number of questions you can select.
* **worst-case space complexity:** `O(1)`.

### Solution 2

* Java
```
public ListNode insertNode(ListNode head, int val) {
    ListNode keyNode = new ListNode(val);
    if(head == null) return keyNode;
    ListNode dummyHead = new ListNode(-1);
    dummyHead.next = head;
    ListNode cur = dummyHead;
    while(cur.next!=null && cur.next.val < val)
        cur = cur.next;
    
    keyNode.next = cur.next;
    cur.next = keyNode;
    
    return dummyHead.next;
}
```

Using a dummy head points to the head of the list.

Always check if the next node value is equal or larger than the `val` where is the node should be inserted.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the `arr`, `k` is the number of questions you can select.
* **worst-case space complexity:** `O(1)`.


