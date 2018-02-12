# LC148. Sort List

### LeetCode

## Question

Sort a linked list in O(n log n) time using constant space complexity.

## Solutions

* C++1 (TLE) quick sort
```
class Solution {
public:
    ListNode* merge(ListNode* left, ListNode* mid,  ListNode* right)
    {
        mid->next = right;
        if(left==NULL) return mid;
        
        ListNode dummy(0);
        dummy.next = left;
        while(left->next!=NULL) left = left->next;
        left->next = mid;
        return dummy.next;
    }
    ListNode* sortList(ListNode* head) {
        if(head == NULL || head->next==NULL) return head;
        ListNode left(0), right(0);
        ListNode *L=&left, *R = &right, *cur=head->next;
        while(cur != NULL)
        {
            if(cur->val <= head->val)
            {
                L->next = cur;
                L = L->next;
            }
            else
            {
                R->next = cur;
                R = R->next;
            }
            cur = cur->next;
        }
        L->next = NULL;
        R->next = NULL;
        return merge(sortList(left.next), head, sortList(right.next));
    }
};
```

* C++2 Divide and conquer
```
class Solution {
public:

    ListNode* merge(ListNode* left, ListNode* right)
    {
        if(left==NULL) return right;
        if(right==NULL) return left;
        if(left->val < right->val)
        {
            left->next = merge(left->next, right);
            return left;
        }
        else
        {
            right->next = merge(left, right->next);
            return right;
        }
    }
    ListNode* sortList(ListNode* head) {
        if(head==NULL || head->next==NULL) return head;
        ListNode *pre, *slow=head, *fast=head;
        while(fast!=NULL && fast->next!=NULL)
        {
            pre = slow;
            slow = slow->next;
            fast = fast->next->next;
        }
        pre->next = NULL;
        return merge(sortList(head), sortList(slow));
    }
};
```

## Explanation

**Solution 1** 

Using Quick Sort algorithm. Separate the list into three lists: a list's values are less or equal than the first node's value, the first node, a list's values are no less than the first node's value. Then, merge the three parts.

**Note:** the idealy time complexity is O(n*log(n)), but in some corner case (have sorted lists) the time complexity is O(n<sup>2</sup>).  

* **worst-case time complexity:** O(n<sup>2</sup>)
* **worst-case space complexity:** O(1)

**Solution 1** 

Using Divide and conquer algorithm. Divide the list into two equal lists. When divide to two single nodes, start to merge and sort the two lists together for upper layer's merge and sort.

* **worst-case time complexity:** O(n*log(n))
* **worst-case space complexity:** O(1)
