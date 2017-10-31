# LC365. Water and Jug Problem

### LeetCode

## Question

You are given two jugs with capacities x and y litres. There is an infinite amount of water supply available. You need to determine whether it is possible to measure exactly z litres using these two jugs.

If z liters of water is measurable, you must have z liters of water contained within one or both buckets by the end.

Operations allowed:

* Fill any of the jugs completely with water.
* Empty any of the jugs.
* Pour water from one jug into another till the other jug is completely full or the first jug itself is empty.

**Example 1:** (From the famous "Die Hard" example)

```
Input: x = 3, y = 5, z = 4
Output: True
```

**Example 2:**

```
Input: x = 2, y = 6, z = 5
Output: False
```

## Solution

* C++1
```
class Solution {
public:
    int GCD(int x, int y)
    {
        return y==0 ? x : GCD(y, x%y);
    }
    bool canMeasureWater(int x, int y, int z) {
        return z <= (long)x + y && z%GCD(x,y) == 0;
    }
};
```

## Explanation

Corner cases:

1. z==0  --> true
2. z > (long)x + y  --> false

**NOTE** the question doesn't limit negative numbers



