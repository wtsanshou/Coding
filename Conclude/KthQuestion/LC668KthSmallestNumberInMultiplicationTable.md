# LC668. Kth Smallest Number in Multiplication Table

### LeetCode (Hard)

## Quesiton

Nearly every one have used the Multiplication Table. But could you find out the k-th smallest number quickly from the multiplication table?

Given the height m and the length n of a m * n Multiplication Table, and a positive integer k, you need to return the k-th smallest number in this table.

**Example 1:**
```
Input: 
m = 3, n = 3, k = 5

Output: 
3

Explanation: 
The Multiplication Table:
1	2	3
2	4	6
3	6	9

The 5-th smallest number is 3 (1, 2, 2, 3, 3).
```

**Example 2:**
```
Input: 
m = 2, n = 3, k = 6

Output: 
6

Explanation: 
The Multiplication Table:
1	2	3
2	4	6

The 6-th smallest number is 6 (1, 2, 2, 3, 4, 6).
```

**Note:**

* The m and n will be in the range [1, 30000].
* The k will be in the range [1, m * n]

## Solutions

### Solution 1

* Java (Memory Limit Exceeded)
```
class Solution {
    public int findKthNumber(int m, int n, int k) {
        int[][] visit = new int[m][n];
        int[] dx = new int[] {1, 0};
        int[] dy = new int[] {0, 1};
        PriorityQueue<Element> pq = new PriorityQueue<>( (a, b) -> Integer.compare(a.val, b.val));
        
        pq.add(new Element(1, 0, 0));
        visit[0][0] = 1;
        
        for(int i = 1; i < k; i++) {
            Element ele = pq.poll();
            for (int j = 0; j < 2; j++) {
                int x = ele.i + dx[j];
                int y = ele.j + dy[j];
                
                if (x < m && y < n && visit[x][y] == 0) {
                    visit[x][y] = j == 0 ? ele.val + visit[0][y]
                                         : ele.val + visit[x][0];
                    pq.add(new Element(visit[x][y], x, y));
                }
            }
        }
            
        return pq.peek().val; 
    }
}

class Element {
    public int val;
    public int i;
    public int j;
    public Element(int val, int i, int j) {
        this.val = val;
        this.i = i;
        this.j = j;
    }
}
```

In this quesiton, `k` could be huge. Using priority queue will be too much memory consumption.

**Complexity:**

* **worst-case time complexity:** `O(k * log(k))`.
* **worst-case space complexity:** `O(m * n)`. 

### Solution 2

Comming soon.
