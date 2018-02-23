# LC738. Monotone Increasing Digits

### LeetCode

## Question

Given a non-negative integer `N`, find the largest number that is less than or equal to `N` with monotone increasing digits.

(Recall that an integer has monotone increasing digits if and only if each pair of adjacent digits `x` and `y` satisfy `x <= y`.)

**Example 1:**
```
Input: N = 10
Output: 9
```

**Example 2:**
```
Input: N = 1234
Output: 1234
```

**Example 3:**
```
Input: N = 332
Output: 299
```

**Note:** 

* N is an integer in the range [0, 10^9].

## Solutions

* Java1
```
public int monotoneIncreasingDigits(int N) {
    int res=0, base=1, pre=N%10;
    N /= 10;
    while(N > 0){
        int cur = N%10;
        N /= 10;
        if(cur > pre){
            res = base * 10 -1;
            pre = cur-1;
        }
        else{
            res += base * pre;
            pre = cur;
        }
        base *= 10;
    }
    res += base * pre;
    return res;
}
```

## Explanation

We need to check the integer `N` from right to left. Once found a digit `x` larger than its right adjacent digit, we need to set all `x`'s right digits to `9` and reduce `1` from the current digit `x`.

* **worst-case time complexity:** O(D), where D is the numbers of digits in `N`.
* **worst-case space complexity:** O(1)