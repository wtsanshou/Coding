# LC29. Divide Two Integers

### LeetCode

## Question

Divide two integers without using multiplication, division and mod operator.
If it is overflow, return MAX_INT.

## Solutions

* C++1
```
int divide(int dividend, int divisor) {
    if(divisor==0 || (dividend==INT_MIN && divisor==-1)) return INT_MAX;
    int res = 0;
    long ldend = labs(dividend), lsor = labs(divisor);
    while(ldend >= lsor)
    {
        long temp = lsor, times=1;
        while(ldend >= (temp<<1))
        {
            temp <<= 1;
            times <<= 1;
        }
        ldend -= temp;
        res += times;
    }
    return dividend<0 ^ divisor<0 ? -res : res;
}
```

## Explanation

`without using multiplication, division and mod operator`, So we only can use `+`, `-`, and bitwise operations

The idea is that we can get the power of 2 times of divisor by `divisor<<1`. So we mins the power of 2 times of divisor from the dividend until the dividend less or equals the divisor.

`If it is overflow, return MAX_INT`, this notice us the overflow corner cases:

1. divisor == 0, result is infinitely great.
2. dividend==-2147483648 && divisor==1, return is 2147483648 which is outside of the `INT_MAX`.

* **worst-case time complexity:** O(log(n))
* **worst-case space complexity:** O(1)
