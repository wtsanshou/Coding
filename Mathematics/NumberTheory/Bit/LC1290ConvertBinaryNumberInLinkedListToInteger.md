# LC1290. Convert Binary Number in a Linked List to Integer

### LeetCode

## Question

Given head which is a reference node to a singly-linked list. The value of each node in the linked list is either 0 or 1. The linked list holds the binary representation of a number.

Return the decimal value of the number in the linked list.

**Example 1:**

```
Input: head = [1,0,1]

Output: 5

Explanation: (101) in base 2 = (5) in base 10
```

**Example 2:**

```
Input: head = [0]

Output: 0
```

**Example 3:**

```
Input: head = [1]

Output: 1
```

**Example 4:**

```
Input: head = [1,0,0,1,0,0,1,1,1,0,0,0,0,0,0]

Output: 18880
```

**Example 5:**

```
Input: head = [0,0]

Output: 0
``` 

**Constraints:**

* The Linked List is not empty.
* Number of nodes will not exceed 30.
* Each node's value is either 0 or 1.

## Solutions

### Solution 1

* Python
```
def getDecimalValue(self, head: ListNode) -> int:
    new_head = self.revert(head)
    result = 0
    power = 0
    while new_head is not None:
        result += new_head.val * (2 ** power)
        power += 1
        new_head = new_head.next
    return result

def revert(self, head: ListNode) -> ListNode:
    left = None
    mid = None
    while head is not None:
        mid = head.next
        head.next = left
        left = head
        head = mid
    return left
```

## Explanation

The first idea is to revert the linked list, then calculate the decimal value.

* **worst-case time complexity:** `O(N)`, where `N` is the length of the linked list `head`.
* **worst-case space complexity:** `O(1)`

### Solution 2

* Python
```
def getDecimalValue(self, head: ListNode) -> int:
    result = 0
    while head:
        result = (result << 1) | head.val
        head = head.next
    return result
```

## Explanation

Just found it can be solved by using bit operation directly.

* **worst-case time complexity:** O(n), where `N` is the length of the linked list `head`.
* **worst-case space complexity:** O(1)
