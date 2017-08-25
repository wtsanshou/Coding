# LC476. Number Complement

### LeetCode

## Question

Given a positive integer, output its complement number. The complement strategy is to flip the bits of its binary representation.

**Note:**

1. The given integer is guaranteed to fit within the range of a 32-bit signed integer.
2. You could assume no leading zero bit in the integer’s binary representation.


**Example 1:**
```
Input: 5
Output: 2
```

**Explanation:**

The binary representation of 5 is 101 (no leading zero bits), and its complement is 010. So you need to output 2.

**Example 2:**
```
Input: 1
Output: 0
```

**Explanation:**

The binary representation of 1 is 1 (no leading zero bits), and its complement is 0. So you need to output 0.

### Solutions

* C++1 (3ms) O(1)
```
int findComplement(int num) {
    int res=0, bit=0;
    while(num > 0)
    {
        res += ((num&1)^1) << bit++;
        num >>= 1;
    }
    return res;
}
```

* Python1
```
def findComplement(self, num):
    i=0
    res = 0
    while num > 0:
        res += ((num&1)^1)<<i
        i=i+1
        num >>= 1
    return res
```

## Explanation

Using 1 ^ each bit of the number

* **worst-case time complexity:** O(32)
* **worst-case space complexity:** O(1)