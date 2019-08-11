# Lint1272. Kth Smallest Element in a Sorted Matrix

### LintCode (Medium)

Given a n x n matrix where each of the rows and columns are sorted in ascending order, find the kth smallest element in the matrix.

**Note that** it is the kth smallest element in the sorted order, not the kth distinct element.

**Example 1**
```
Input:
[[ 1,  5,  9],[10, 11, 13],[12, 13, 15]]
8

Output: 
13
```

**Example 2**
```
Input:
[[-5]]
1

Output: 
-5
```

**Challenge**

* If k << n^2, what's the best algorithm?
* How about k ~ n^2?

**Notice**

* You may assume k is always valid, 1 ≤ k ≤ n^2.

## Solutions

### Solution 1

* Java
```
public class Solution {
    /**
     * @param matrix: List[List[int]]
     * @param k: a integer
     * @return: return a integer
     */
    public int kthSmallest(int[][] matrix, int k) {
        int[] dx = new int[] {1, 0};
        int[] dy = new int[] {0, 1};
        int h = matrix.length;
        int w = matrix[0].length;
        boolean[][] visit = new boolean[h][w];
        
        PriorityQueue<Element> pq = new PriorityQueue<>(new Comparator<Element>(){
            public int compare(Element a, Element b) {
                return Integer.compare(a.val, b.val);
            }
        });
        pq.add(new Element(matrix[0][0], 0, 0));
        
        for (int i = 1; i < k; i++) {
            Element min = pq.remove();
            for (int j = 0; j < 2; j++) {
                int x = min.i + dx[j];
                int y = min.j + dy[j];
                
                if (x < h && y < w && visit[x][y] == false) {
                    visit[x][y] = true;
                    pq.add(new Element(matrix[x][y], x, y)); 
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

Using a priority queue `pq` to maintain the current candidates. Take the minimum element `min` from the `pq`, and based on the `min`, put new candidates into the `pq`. repeat this process `k` times, the peek of the `pq` will be the Kth smallest element in the sorted matrix.

**Note**

1. Put the `matrix[0][0]` into the `pq` at the beginning.
2. Need to keep the location of the candidates, so create a class `Element`.
3. Need a map `visit` to remember the visited elements in order to avoid putting candidates multiple times.

**Link**

Two more questions with the same solution

* Kth Smallest Number Sum In Two Array
* Kth Smallest Number Product In Two Array

The `Sum` or `Product` could be transfered to a `matrix`.

**Complexity:**

* **worst-case time complexity:** `O(k * log(k))`.
* **worst-case space complexity:** `O(h * w)`, where `h` is the height of the `matrix`, `w` is the width of the `matrix`. 
