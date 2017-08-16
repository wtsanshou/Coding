# LC400. Nth Digit

### LeetCode

## Question

Find the nth digit of the infinite integer sequence 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, ...

**Note:**

n is positive and will fit within the range of a 32-bit signed integer (n < 231).

**Example 1:**

**Input:**
```
3
```

**Output:**
```
3
```

**Example 2:**

**Input:**
```
11
```

**Output:**
```
0
```

Explanation:

The 11th digit of the sequence 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, ... is a 0, which is part of the number 10.

## Solutions

* C++1 (3ms)
```
int findNthDigit(int n) {
        int len=1,  start =1;
        long count = 9;
        while(n > len*count)
        {
            n -= len*count; //minus the length of a kind of number (1 digit, 2 digits,….)
            len++;          // (1 digit, 2 digits,….)
            count *= 10;    //the count of the same size of digit number (9, 90 ,900, …)
            start *= 10;    //the start number of the same digit number (1, 10, 100…)
        }
        start += (n-1)/len;
        string res = to_string(start);
        return res[(n-1)%len] - '0';
    }
```

## Explanation

1. Count from the first number (1, 10, 100, ...) of each digital size (1, 2, 3, ...)
2. Find the biggest first number of n.
3. The result is the end digit of the number `the biggest first number` + `the rest of n`.

* **worst-case time complexity:** O(1)
* **worst-case space complexity:** O(1)