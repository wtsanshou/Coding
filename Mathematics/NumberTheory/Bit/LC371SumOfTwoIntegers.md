# LC371. Sum of Two Integers

### LeetCode

## Question

Calculate the sum of two integers a and b, but you are not allowed to use the operator + and -.

Example:

Given a = 1 and b = 2, return 3.

## Solutions

* C++1
```
int getSum(int a, int b) {
    if(b==0) return a;
    int carry = (a&b)<<1;
    int sum = a^b;
    return getSum(sum, carry);
}
```

* C++2
```
int getSum(int a, int b) {
    if(b==0) return a;
    return getSum(a^b, (a&b)<<1);
}
```

* Java1
```
int getSum(int a, int b) {
    if(b==0) return a;
    return getSum(a^b, (a&b)<<1);
}
```

* Python1
```
def getSum(self, a, b):
    MAX = 0x7fffffff
    MIN = 0x80000000
    mask = 0xffffffff
    while b != 0:
        a, b = (a^b) & mask, ((a&b)<<1) & mask
    return a if a<=MAX else ~(a ^ mask)
```

* Python2
```
def getSum(self, a, b):
    MAX = 0x7fffffff
    MIN = 0x80000000
    mask = 0xffffffff
    for _ in range(32):
        a, b = a^b, (a&b)<<1
    return a if a&MIN > 0 else a & MAX
```

## Explanation

a^b = binary sum of a and b but ignore carry.
(a&b) << 1 = the carry of a binary add b

* **worst-case time complexity:** O(log(n))
* **worst-case space complexity:** O(1)