# LC191. Number of 1 Bits

### LeetCode

## Question

Write a function that takes an unsigned integer and returns the number of `1` bits it has (also known as the Hamming weight).

For example, the 32-bit integer `11` has binary representation `00000000000000000000000000001011`, so the function should return 3.

## Solutions

* C++1
```
int hammingWeight(uint32_t n) {
        int count=0;
        while(n > 0)
        {
            count++;
            n &= (n-1);
        }
        return count;
}
```

* Java1
```
// you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        int count=0;
        while(n!=0)
        {
            count++;
            n = n&(n-1);
        }
        return count;
    }
```

## Explanation

n&(n-1) remove the very right binary `1` of the number n.

* **worst-case time complexity:** O(32)
* **worst-case space complexity:** O(1)