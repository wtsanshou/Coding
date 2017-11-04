# LC172. Factorial Trailing Zeroes

### LeetCode

##Question

Given an integer n, return the number of trailing zeroes in n!.

**Note:** Your solution should be in logarithmic time complexity.

## Solutions

* C++ (3ms)
```
int trailingZeroes(int n) {
    return (n==0) ? 0 : n/5 + trailingZeroes(n/5);
}
```

## Explanation

From 1, 2, 3, 4, 5,..., 9, only multiply `5` could get trailing zero.

From the n factorial, 1, 2, 3,..., n, we just need to find how many `5` in the n factorial.

**NOTE** `5*5` has `2` `5` in the n factorial,...,  5<sup>x</sup> has `x` `5` in the n factorial.

* **worst-case time complexity:** O(log<sub>5</sub>(n))
* **worst-case space complexity:** O(log<sub>5</sub>(n))