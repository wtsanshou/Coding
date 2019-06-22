# LC504. Base 7

### LeetCode

## Question

Given an integer, return its base 7 string representation.

**Example 1:**

```
Input: 100
Output: "202"
```

**Example 2:**

```
Input: -7
Output: "-10"
```

**Note:** The input will be in range of [-1e7, 1e7].

## Solutions

* C++1 (6ms)
```
string convertToBase7(int num) {
    if(num == 0) return "0";
    int base = abs(num);
    string res;
    while(base != 0)
    {
        res = to_string(base%7) + res;
        base /= 7;
    }
    return (num>0) ? res : "-"+res;
}
```

* C++2 (9ms)
```
class Solution {
public:
    string myRescursive(int num)
    {
        if(num==0) return "";
        return myRescursive(num/7) + to_string(num%7);
    }
    string convertToBase7(int num) {
        if(num==0) return "0";
        return ((num>0) ? "" : "-") + myRescursive(abs(num));
    }
};
```

## Explanation

The input will be in range of [-1e7, 1e7], don't need to worry -2147483648.

* **worst-case time complexity:** O(log<sub>7</sub>(n)), where `n` is `num`.
* **worst-case space complexity:** O(1)