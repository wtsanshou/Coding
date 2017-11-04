# LC693. Binary Number with Alternating Bits

### LeetCode

## Question

Given a positive integer, check whether it has alternating bits: namely, if two adjacent bits will always have different values.

**Example 1:**

```
Input: 5
Output: True
Explanation:
The binary representation of 5 is: 101
```

**Example 2:**

```
Input: 7
Output: False
Explanation:
The binary representation of 7 is: 111.
```

**Example 3:**

```
Input: 11
Output: False
Explanation:
The binary representation of 11 is: 1011.
```

**Example 4:**

```
Input: 10
Output: True
Explanation:
The binary representation of 10 is: 1010.
```

## Solutions

* C++1
```
bool hasAlternatingBits(int n) {
    int pre = n & 1;
    while((n>>=1) > 0){
        int cur = n & 1;
        if(!pre^cur) return false;
        pre = cur;
    }
    return true;
}
```

## Explanation

Bitwise XOR adjacent bits.

* **worst-case time complexity:** O(log(n))
* **worst-case space complexity:** O(1)



