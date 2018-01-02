# LC382. Linked List Random Node

### LeetCode

## Question

Given a singly linked list, return a random node's value from the linked list. Each node must have the same probability of being chosen.

**Follow up** What if the linked list is extremely large and its length is unknown to you? Could you solve this efficiently without using extra space?

**Example:**

```
// Init a singly linked list [1,2,3].
ListNode head = new ListNode(1);
head.next = new ListNode(2);
head.next.next = new ListNode(3);
Solution solution = new Solution(head);
```

```
// getRandom() should return either 1, 2, or 3 randomly. Each element should have equal probability of returning.
solution.getRandom();
```

```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(head);
 * int param_1 = obj.getRandom();
 */
```

## Solutions

* C++1 (49ms)
```
class Solution {
private:
    ListNode* list;
public:
    /** @param head The linked list's head.
        Note that the head is guaranteed to be not null, so it contains at least one node. */
    Solution(ListNode* head) {
        list = head;
    }
    
    /** Returns a random node's value. */
    int getRandom() {
        int res = list->val;
        ListNode* cur = list;
        for(int i=1; cur!=NULL; ++i)
        {
            if(rand()%i == 0) res = cur->val;
            cur = cur->next;
        }
        return res;
    }
};
```

* C++2
```
class Solution {
private:
    vector<int> values;
    int size;
public:
    /** @param head The linked list's head. Note that the head is guanranteed to be not null, so it contains at least one node. */
    Solution(ListNode* head) {
        while(head!=NULL)
        {
            values.push_back(head->val);
            head = head->next;
        }
        size = values.size();
        srand(time(NULL));
    }
    
    /** Returns a random node's value. */
    int getRandom() {
        return values[rand()%size];
    }
};
```

* Java1
```
public class Solution {

    private ListNode myHead;
    private Random rand;
    
    /** @param head The linked list's head.
        Note that the head is guaranteed to be not null, so it contains at least one node. */
    public Solution(ListNode head) {
        myHead = head;
        rand = new Random();
    }
    
    /** Returns a random node's value. */
    public int getRandom() {
        ListNode node = myHead;
        ListNode res = node;
        for (int i=1; node != null; ++i)
        {
            if(rand.nextInt(i) == 0) //if((int)(Math.random()*i) == 0)
                res = node;
            node = node.next;
        }
        return res.val;
    }
}
```

* Java2
```
public class Solution {
    private List<Integer> values;
    private int size;
    private Random random;
    /** @param head The linked list's head. Note that the head is guanranteed to be not null, so it contains at least one node. */
    public Solution(ListNode head) {
        values = new ArrayList<Integer>();
        while(head!=null)
        {
            values.add(head.val);
            head = head.next;
        }
        size = values.size();
        random = new Random();
    }
    
    /** Returns a random node's value. */
    public int getRandom() {
        return values.get(random.nextInt(size));
    }
}
```

## Explanation

The simplest solution is to use an array to store the link list values. Then, getting random index of the array to find the result.

* **worst-case time complexity:** O(1)
* **worst-case space complexity:** O(n)

**Follow up**  What if the linked list is extremely large and its length is unknown to you? Could you solve this efficiently without using extra space?

As explained in <a href="https://en.wikipedia.org/wiki/Harmonic_series_(mathematics)">Harmonic series</a>, to get the equal probability, we need to travel the array and count the target. For each target index, it has `1/count` probability to be the result.

![HarmonicSeries](Images/HarmonicSeries.tiff)

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)