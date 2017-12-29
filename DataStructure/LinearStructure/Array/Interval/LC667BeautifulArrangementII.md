# LC667. Beautiful Arrangement II

### LeetCode

## Question

Given two integers n and k, you need to construct a list which contains n different positive integers ranging from 1 to n and obeys the following requirement: 

Suppose this list is `[a1, a2, a3, ... , an]`, then the list `[|a1 - a2|, |a2 - a3|, |a3 - a4|, ... , |an-1 - an|]` has exactly `k` distinct integers.

If there are multiple answers, print any of them.

**Example 1:**

```
Input: n = 3, k = 1
Output: [1, 2, 3]
```

**Explanation:** 

The [1, 2, 3] has three different positive integers ranging from 1 to 3, and the [1, 1] has exactly 1 distinct integer: 1.

**Example 2:**

```
Input: n = 3, k = 2
Output: [1, 3, 2]
```

**Explanation:** 

The [1, 3, 2] has three different positive integers ranging from 1 to 3, and the [2, 1] has exactly 2 distinct integers: 1 and 2.

**Note:**

* The n and k are in the range 1 <= k < n <= 10<sup>4</sup>.

## Solutions

* C#1
```
public int[] ConstructArray(int n, int k) {
    int f = n-k;
    int[] res = new int[n];
    for(int i=0; i<f; ++i){
        res[i] = i+1;
    }
    for(int i=0; i<n-f; ++i){
        if(i%2 == 0)
            res[f+i] = n-(i/2);
        else
            res[f+i] = f+(i/2)+1;
    }
    return res;
}
```

## Explanation

`n` continue positive integers from 1 to n, needs `k` distinct intervals. So there must be `n-k-1` same intervals.

If input is `n` `n-1`, the result must be unique.

My idea is to arrange `n-k-1` **1** intervals, `k-1` intervals from **2** to **k**.

`n-k-1` **1** intervals is easy to get: `1, 2, 3, ..., f`.  Where `f = n-k`

To find `k-1` intervals from **k** to **2**:

```
Intervals:1 1   ...    1    k      k-1      k-2      k-3      ...     2    1
Array:   1 2 3  ...f-1  f       n      f+1       n-1    f+2   ...     
Index:   0 1 2  ...f-2 f-1      f      f+1       f+2    f+3   ...  n-3  n-2    n-1
```

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(n)