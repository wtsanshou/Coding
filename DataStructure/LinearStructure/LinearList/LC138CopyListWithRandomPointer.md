# LC138. Copy List with Random Pointer

### LeetCode

## Question

A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.

## Solutions

* C++1
```
RandomListNode *copyRandomList(RandomListNode *head) {
    RandomListNode *newHead, *p1, *p2;
    if(head==nullptr) return nullptr;
    //create list p2, and link p2 in p1 //1->1->2->2->3->3...
    for(p1=head; p1!=nullptr; p1=p1->next->next)
    {
        p2 = new RandomListNode(p1->label);
        p2->next = p1->next;
        p1->next = p2;
    } 
    //copy random from p1 to p2
    for(p1=head; p1!=nullptr; p1 = p1->next->next)
    {
        p2 = p1->next;
        if(p1->random!=nullptr) p2->random = p1->random->next;
    } 
    //cut p1 and p2
    newHead = head->next;
    for(p1=head; p1!=nullptr; p1=p1->next)
    {
        p2 = p1->next;
        p1->next = p2->next;
        if(p1->next!=nullptr) p2->next = p1->next->next;
    } 
    return newHead;
}
```

## Explanation

Step 1: create list p2, and link p2 in p1
```
p1: 1       2       3       4       5   ...
     \    /  \    /   \    /  \    / \
      \  /    \  /     \  /    \  /   \
p2      1       2       3       4       5
```

Step 2: copy random from p1 to p2
```
p1:         1       2       3       4       5   ...
             \    /  \    /   \    /  \    / \
              \  /    \  /     \  /    \  /   \
p2:             1       2       3       4       5
                |       |       |       |       |       
                |       |       |       |       |
p1->random:     1->r    2->r    3->r    4->r    5->r
```

Step 3: Cut p1 from p2 and connect p2 list.
```
p1:         1       2       3       4       5   ...


p2:             1------>2------>3------>4------>5
                |       |       |       |       |       
                |       |       |       |       |
p1->random:     1->r    2->r    3->r    4->r    5->r
```

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)