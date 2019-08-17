# Lint390. Find Peak Element II

### LintCode (Hard)

## Question

Given an integer matrix A which has the following features :

The numbers in adjacent positions are different.
The matrix has n rows and m columns.
For all i < n, A[i][0] < A[i][1] && A[i][m - 2] > A[i][m - 1].
For all j < m, A[0][j] < A[1][j] && A[n - 2][j] > A[n - 1][j]
We define a position [i, j] is a peak if:

```
  A[i][j] > A[i + 1][j] && A[i][j] > A[i - 1][j] && 
  A[i][j] > A[i][j + 1] && A[i][j] > A[i][j - 1]
```

Find a peak element in this matrix. Return the index of the peak.


**Example 1:**
```
Input: 
    [
      [1, 2, 3, 6,  5],
      [16,41,23,22, 6],
      [15,17,24,21, 7],
      [14,18,19,20,10],
      [13,14,11,10, 9]
    ]

Output: 
[1,1]

Explanation: 
[2,2] is also acceptable. The element at [1,1] is 41, greater than every element adjacent to it.
```

**Example 2:**
```
Input: 
    [
      [1, 5, 3],
      [4,10, 9],
      [2, 8, 7]
    ]

Output: 
[1,1]

Explanation: 
There is only one peek.
```

**Challenge**

* Solve it in O(n+m) time.

If you come up with an algorithm that you thought it is O(nlog(m)) or O(mlog(n)), can you prove it is actually O(n+m) or propose a similar but O(n+m) algorithm?

**Notice**

Guarantee that there is at least one peak, and if there are multiple peaks, return any one of them.

## Solutions

### Solution 1

* Java
```
public class Solution {
    /*
     * @param A: An integer matrix
     * @return: The index of the peak
     */
    public List<Integer> findPeakII(int[][] A) {
        int h = A.length;
        int w = A[0].length;
        int i = 0, j = h - 1;
        
        Peak peak = new Peak(0, 0, A[0][0]);
        
        while (i <= j) {
            int mid = i + (j - i) / 2;
            Peak curHighest = findHighestInTheRow(A, mid);
            
            if (curHighest.height > peak.height)
                peak = curHighest;
            
            if(mid > 0 && mid < h - 1 && A[mid - 1][curHighest.j] < curHighest.height && curHighest.height > A[mid + 1][curHighest.j]) {
                peak = curHighest;
                break;
            }
            
            if (mid == h - 1 || mid > 0 && A[mid - 1][curHighest.j] > curHighest.height) {
                j = mid - 1;
                continue;
            }
            
            if (mid == 0 || mid < h - 1 && A[mid + 1][curHighest.j] > curHighest.height)
                i = mid + 1;
        }
        
        return Arrays.asList(peak.i, peak.j);
    }
    
    private Peak findHighestInTheRow(int[][] A, int mid) {
        Peak curHighest = new Peak(mid, 0, A[mid][0]);
        for (int k = 1; k < A[0].length; k++) {
            if (A[mid][k] > curHighest.height) {
                curHighest = new Peak(mid, k, A[mid][k]);
            }
        }
        return curHighest;
    }
}

class Peak {
    int i, j, height;
    public Peak(int i, int j, int height) {
        this.i = i;
        this.j = j;
        this.height = height;
    }
}
```

The idea is to use binary search to locate the middle row of the searching range. In the middle row, find the highest point `curHighest`, compare the up and down points with the `curHighest`, narrow the searching range to the higher direction. 

We can imaging the middle row is a `wall` with the same height of the `curHighest`, so that the search range would never cross the `wall` again.

**Complexity:**

* **worst-case time complexity:** `O(w * log(h))`, where `w` is the width of the `A`, `h` is the height of the `A`.
* **worst-case space complexity:**  `O(1)`.

### Solution 2

For `O(w + h)` time complexity solution, We need to alternatly binary search row and column.

So the time consume is:

```
w + h/2 + w/2 + h/4 + w/4 + h/8 + w/8 + ... + h/(2^m) + w/(2^n)
= w + w/2 + w/4 + w/8 + ... + w/(2^n)
    + h/2 + h/4 + h/8 + ... + h/(2^m)
= w * (1 + 1/2 + 1/4 + 1/8 + ... + 1/(2^n)
+ h * (1/2 + 1/4 + 1/8 + ... + 1/(2^m))

= O(w + h)
```

**Where **

* `(1 + 1/2 + 1/4 + 1/8 + ... + 1/(2^n)` < 2
* 2<sup>n</sup> <= w
* `(1/2 + 1/4 + 1/8 + ... + 1/(2^m))` < 1
* 2<sup>m</sup> <= h

**Complexity:**

* **worst-case time complexity:** `O(w + h)`, where `w` is the width of the `A`, `h` is the height of the `A`.
* **worst-case space complexity:**  `O(1)`.