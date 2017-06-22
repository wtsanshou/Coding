# 263. Ugly Number

### LeetCode

## Question

Write a program to check whether a given number is an ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5. For example, 6, 8 are ugly while 14 is not ugly since it includes another prime factor 7.

Note that 1 is typically treated as an ugly number.

## Solutions

* C++1
```
bool isUgly(int num) {
        if(num<=0) return false;
        int primes[3] = {2,3,5};
        for(int i=0; i<3; ++i)
        {
            if(num % primes[i] == 0)
            {
                num /= primes[i--];
            }
        }
        return num==1;
    }
```

## Explanation

The idea is to check if the `num` can be divided by 2, 3, 5 until 1, no matter how many 2, 3, or 5.

**Corner Cases:**

1. num <= 0
2. num = 1

* **worst-case time complexity:** O(log(n))
* **worst-case space complexity:** O(1)
