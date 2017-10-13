# LC201. Bitwise AND of Numbers Range

### LeetCode

## Question

Given a range [m, n] where `0 <= m <= n <= 2147483647`, return the bitwise `AND` of all numbers in this range, inclusive.

For example, given the range [5, 7], you should return 4.

## Solutions

* C++1
```
int rangeBitwiseAnd(int m, int n) {
    while(m<n) n = n&(n-1);
    return n;
}
```

* C++2 (25ms) beat 95%
```
int rangeBitwiseAnd(int m, int n) {
    if(m>=n) return n;
    return rangeBitwiseAnd(m, n&(n-1));
}
```

* C++3
```
int rangeBitwiseAnd(int m, int n) {
    return (m>=n) ? n : rangeBitwiseAnd(m, n&(n-1));
}
```

* C++4
```
int rangeBitwiseAnd(int m, int n) {
    int trans = 0;
    while(m!=n)
    {
        trans++;
        m>>=1;
        n>>=1;
    }
    return m<<trans;
}
```

* C++5
```
int rangeBitwiseAnd(int m, int n) {
    return (m < n)? (rangeBitwiseAnd(m/2, n/2)<<1) : m;
}
```

## Explanation

The most straight forward way is to bitwide `AND` all the numbers from n to m, no matter iteration or recursive.

* **worst-case time complexity:** O(n-m)

If we comapre the final result with m and n, we can see the result is the left part bits of m and n where they have the save bits. Because the right part would become `0`s after bitwide `AND` all the numbers from n to m

**Example 1** 

```
5 : 101
7 : 111
----------
4 : 100
```

* **worst-case time complexity:** O(log(n))
* **worst-case space complexity:** O(1)