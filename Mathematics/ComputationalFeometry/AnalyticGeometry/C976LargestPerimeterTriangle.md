# LC976. Largest Perimeter Triangle

### LeetCode

## Question

Given an array A of positive lengths, return the largest perimeter of a triangle with non-zero area, formed from 3 of these lengths.

If it is impossible to form any triangle of non-zero area, return 0.

**Example 1:**
```
Input: [2,1,2]
Output: 5
```

**Example 2:**
```
Input: [1,2,1]
Output: 0
```

**Example 3:**
```
Input: [3,2,3,4]
Output: 10
```

**Example 4:**
```
Input: [3,6,2,3]
Output: 8
```

**Note:**

* 3 <= A.length <= 10000
* 1 <= A[i] <= 10^6

## Solutions

* Java1
```
public int largestPerimeter(int[] A) {
    Arrays.sort(A);
    for(int i=A.length-1; i>1; --i)
        if(A[i-1]+A[i-2] > A[i]) return A[i-1] + A[i-2] + A[i];
    return 0;
}
```

## Explanation

To be a triangle, the sum of any two sides must be larger than the third side.

The largest perimeter of a triangle must be the biggest 3 sides who match the triangle rule.

* **worst-case time complexity:** `O(n*log(n))`, where `n` is the number of the array `A`.
* **worst-case space complexity:** `O(n*log(n))`, where `n` is the number of the array `A`.
