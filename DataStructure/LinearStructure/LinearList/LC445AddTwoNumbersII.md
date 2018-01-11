# LC445. Add Two Numbers II

### LeetCode

## Question

You are given two non-empty linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.
You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Follow up:** What if you cannot modify the input lists? In other words, reversing the lists is not allowed.

**Example:**

```
Input: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 8 -> 0 -> 7
```

## Solutions

* C++1 (49ms) using stack
```
ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        stack<int> s1, s2;
        while(l1!=NULL)
        {
            s1.push(l1->val);
            l1 = l1->next;
        }
        while(l2!=NULL)
        {
            s2.push(l2->val);
            l2 = l2->next;
        }
        ListNode* head = new ListNode(0);
        while(!s1.empty() || !s2.empty())
        {
            int a=0, b=0;
            if(!s1.empty())
            {
                a = s1.top();
                s1.pop();
            }
            if(!s2.empty())
            {
                b = s2.top();
                s2.pop();
            }
            int sum = a + b + head->val;
            ListNode* carry = new ListNode(sum/10);
            head->val = sum%10;
            carry->next = head;
            head = carry;
        }
        return (head->next==NULL || head->val!=0) ? head : head->next;
}
```

* C++2 reverse both of them

## Explanation

If we reverse both of them, then we can see the question <a href="LC2AddTwoNumbers.md">LC2. Add Two Numbers</a>.

If we cannot modify the input lists, we can use two stacks to store the two numbers. Then add the two number from the two stacks.

* **worst-case time complexity:** O(MaxLen(l1, l2))
* **worst-case space complexity:** O(MaxLen(l1, l2))