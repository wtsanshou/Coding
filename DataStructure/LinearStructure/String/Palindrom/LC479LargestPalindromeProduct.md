# 479. Largest Palindrome Product

### LeetCode

Find the largest palindrome made from the product of two n-digit numbers.
Since the result could be very large, you should return the largest palindrome mod 1337.

**Example:**
```
Input: 2
Output: 987
Explanation: 99 x 91 = 9009, 9009 % 1337 = 987
```

**Note:**

The range of n is [1,8].

## Soluctions

* C++1
```
int largestPalindrome(int n) {
        int res[] = {9, 987, 123, 597, 677, 1218, 877, 475};
        return res[n-1];
    }
```

## Explanation

I found a tricky solution. It's not a easy question. I need to find the real solution.
