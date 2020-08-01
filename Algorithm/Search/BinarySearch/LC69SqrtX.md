# LC69. Sqrt X

### LeetCode

## Quesiton

Implement int sqrt(int x).

Compute and return the square root of x, where x is guaranteed to be a non-negative integer.

Since the return type is an integer, the decimal digits are truncated and only the integer part of the result is returned.

**Example 1:**
```
Input: 4
Output: 2
```

**Example 2:**
```
Input: 8
Output: 2
Explanation: The square root of 8 is 2.82842..., and since 
             the decimal part is truncated, 2 is returned.
```

## Solutions

### Solution 1

* Python
```
def mySqrt(self, x: int) -> int:
    if x <= 1:
        return x
    return self.find_sqrt(x, 1, x)

def find_sqrt(self, target: int, i: int, j: int):
    if i > j:
        return j
    mid = i + int((j - i) / 2)
    if mid ** 2 == target:
        return mid
    elif mid ** 2 > target:
        return self.find_sqrt(target, i, mid - 1)
    else:
        return self.find_sqrt(target, mid + 1, j)
```

* Python
```
def mySqrt(self, x: int) -> int:
    if x <= 1:
        return x
    i = 1
    j = x
    while i <= j:
        mid = i + int((j - i) / 2)
        if mid ** 2 == x:
            return mid
        elif mid ** 2 > x:
            j = mid - 1
        else:
            i = mid + 1
    return j
```

**Explanation**

Uing binary search to find the closest sqrt `x`.

**Complexity:**

* **worst-case time complexity:** `O(log(x))`.
* **worst-case space complexity:** `O(log(x))` if using recursive

