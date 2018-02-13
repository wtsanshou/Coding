# LC143. Reorder List

### LeetCode

## Question

Given a singly linked list L: `L0→L1→…→Ln-1→Ln`, reorder it to: `L0→Ln→L1→Ln-1→L2→Ln-2→…`

You must do this in-place without altering the nodes' values.

For example, Given `{1,2,3,4}`, reorder it to `{1,4,2,3}`.

## Solutions

* C++1
```
class Solution {
public:
    ListNode* reverse(ListNode* head)
    {
        if(head==NULL|| head->next==NULL) return head;
        ListNode* pre=head, *cur= head->next;
        pre->next=NULL;
        while(cur!=NULL)
        {
            head = cur->next;
            cur->next=pre;
            pre = cur;
            cur = head;
        }
        return pre;
    }
    void combine(ListNode* left, ListNode* right)
    {
        if(left==NULL || right==NULL) return;
        ListNode* next=left->next;
        left->next=right;
        combine(right, next);
    }
    void reorderList(ListNode* head) {
        if(head==NULL || head->next==NULL) return;
        ListNode* left=head, *right=head;
        while(right!=NULL && right->next!=NULL)
        {
            left = left->next;
            right = right->next->next;
        }
        right = left->next;
        left->next=NULL;
        left = head;
        right = reverse(right);
        combine(left, right);
    }
};
```

* C++2
```
void reorderList(ListNode* head) {
        if(head==NULL || head->next==NULL) return;
        ListNode* p1=head, *p2=head->next, *head2;
        
        //find mid
        while(p2!=NULL && p2->next!=NULL)
        {
            p1=p1->next;
            p2=p2->next->next;
        }
        
        //cut half
        head2 = p1->next;
        p1->next = NULL;
        
        //reverse right half
        p2 = head2->next;
        head2->next = NULL;
        while(p2!=NULL)
        {
            p1 = p2->next;
            p2->next = head2;
            head2 = p2;
            p2 = p1;
        }
        
        //merge left half and right half
        for(p1=head, p2 = head2; p1;)
        {
            head2 = p1->next;
            p1->next = p2;
            p1 = p1->next;
            p2 = head2;
        }
    }
```

## Explanation

1. Cut the list in the middle.
2. Reverse the right half list.
3. Merge the two lists' nodes one by one.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)