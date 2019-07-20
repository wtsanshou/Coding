# Lint75. Find Peak Element

### LintCode

## Question

There is an integer array which has the following features:

The numbers in adjacent positions are different.

`A[0] < A[1] && A[A.length - 2] > A[A.length - 1]`

We define a position P is a peak if:

`A[P] > A[P-1] && A[P] > A[P+1]`

Find a peak element in this array. Return the index of the peak.

**Example 1:**
```
Input:  
[1, 2, 1, 3, 4, 5, 7, 6]

Output:  
1 or 6

Explanation:
return the index of peek.
```

**Example 2:**
```
Input: 
[1,2,3,4,1]

Output:  
3
```

**Challenge**

* Time complexity `O(logN)`

**Notice**

* It's guaranteed the array has at least one peak.

## Solutions

### Solution 1

* Java
```
public int findPeak(int[] A) {
    int i = 0, j = A.length-1;
    while (i < j) {
        int mid = i + (j - i) / 2;
        if (A[mid - 1] < A[mid] && A[mid] > A[mid + 1])
            return mid;
        else {
            if (A[mid - 1] > A[mid + 1])
                j = mid - 1;
            else    
                i = mid + 1;
        }
    }
    return i;
}
```

Checking each position is the most straight forward solution for this quesiton. But it's `O(n)` time complexity.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `A`.
* **worst-case space complexity:** `O(1)`.

### Solution 2

* Java
```
public int findPeak(int[] A) {
    int i = 0, j = A.length-1;
    while (i < j) {
        int mid = i + (j - i) / 2;
        if (A[mid - 1] < A[mid] && A[mid] > A[mid + 1])
            return mid;
        else {
            if (A[mid - 1] > A[mid + 1])
                j = mid - 1;
            else    
                i = mid + 1;
        }
    }
    return i;
}
```

To reach `O(log(n))`, we need to use binary search. The peek point must be a bigger number than it's neighbours. So we just need to narrow the `i` and `j` range to always include the bigger number.

**Complexity:**

* **worst-case time complexity:** `O(log(n))`, where `n` is the length of the input `A`.
* **worst-case space complexity:** `O(1)`.
