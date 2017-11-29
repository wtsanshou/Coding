# LC202. Happy Number

### LeetCode

## Question

Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

**Example:** 19 is a happy number


* 1<sup>2</sup> + 9<sup>2</sup> = 82
* 8<sup>2</sup> + 2<sup>2</sup> = 68
* 6<sup>2</sup> + 8<sup>2</sup> = 100
* 1<sup>2</sup> + 0<sup>2</sup> + 0<sup>2</sup> = 1


## Solutions

* C++1 (3ms)
```
bool isHappy(int n) {
    while(n>6)
    {
        int sum = 0;
        while(n>0)
        {
            int digit = n%10;
            n/=10;
            sum += digit*digit;
        }
        n = sum;
    }
    return n==1;
}
```

## Explanation

1. `1` is a happy number.
2. If n!=1 and n<6, n is not a happy number.
3. if n>=6, after the process, it will loop to a number less than 6 in somewhere.
