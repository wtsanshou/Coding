# LC725. Split Linked List in Parts

### LeetCode

## Question

Given a (singly) linked list with head node root, write a function to split the linked list into k consecutive linked list "parts".

The length of each part should be as equal as possible: no two parts should have a size differing by more than 1. This may lead to some parts being null.

The parts should be in order of occurrence in the input list, and parts occurring earlier should always have a size greater than or equal parts occurring later.

Return a List of ListNode's representing the linked list parts that are formed.

Examples 1->2->3->4, k = 5 // 5 equal parts [ [1], [2], [3], [4], null ]

**Example 1:**
```
Input:  
root = [1, 2, 3], k = 5 

Output: 
[[1],[2],[3],[],[]] 
```

**Explanation:**

The input and each element of the output are ListNodes, not arrays. For example, the input root has root.val = 1, root.next.val = 2, \root.next.next.val = 3, and root.next.next.next = null. The first element output[0] has output[0].val = 1, output[0].next = null. The last element output[4] is null, but it's string representation as a ListNode is []. 


**Example 2:**
```
Input: 
root = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10], k = 3

Output: 
[[1, 2, 3, 4], [5, 6, 7], [8, 9, 10]]
```

**Explanation:**

The input has been split into consecutive parts with size difference at most 1, and earlier parts are a larger size than the later parts.

**Note:**

* The length of root will be in the range [0, 1000].
* Each value of a node in the input will be an integer in the range [0, 999].
* k will be an integer in the range [1, 50].

## Solutions

* Java1
```
class Solution {
    public ListNode[] splitListToParts(ListNode root, int k) {
        int len = getLen(root);
        int p = len/k, j=0;
        ListNode[] res = new ListNode[k];
        if(root==null) return res;
        if(p!=0 && p*k != len){
            for(int i=0; i<len%k; ++i)
                root = putAResult(res, j++, root, p+1);
        }
        if(p==0) p += 1;
        for(; j<k; ++j){
            root = putAResult(res, j, root, p);
        }
        return res;
    }
    
    private int getLen(ListNode root){
        int count=0;
        for(ListNode cur=root; cur!=null; cur=cur.next)
            count++;
        return count;
    }
    
    private ListNode putAResult(ListNode[] res, int j, ListNode root, int size){
        ListNode dummy = new ListNode(0);
        ListNode pre = dummy;
        for(int i=0; i<size && root!=null; ++i){
            ListNode cur = new ListNode(root.val);
            pre.next = cur;
            pre = cur;
            root = root.next;
        }
        res[j] = dummy.next;
        return root;
    }
}
```

## Explanation

1. Get the length `len` of the list.
2. Chect how many nodes should put in each part.

* root is null, all parts are null
* list can be evenly splited into `k` parts, put `len/k` nodes in each part.
* len < k, and list cannot be evenly splited into `k` parts, put `len/k + 1` nodes into the first `len%k` parts, put `len/k` nodes into the rest parts.
* len > k, put 1 node into the first 'k' parts, null for the rest parts.

* **worst-case time complexity:** O(max(len, k))
* **worst-case space complexity:** O(k)