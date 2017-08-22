# LC190. Reverse Bits

### LeetCode

## Question

Reverse bits of a given 32 bits unsigned integer.

For example, given input **43261596** (represented in binary as `00000010100101000001111010011100`), return **964176192** (represented in binary as `00111001011110000010100101000000`).

**Follow up:**

If this function is called many times, how would you optimize it?

## Solutions

* C++1 (3ms) O(1)
```
uint32_t reverseBits(uint32_t n) {
        uint32_t res = 0;
        for(int i=0; i<32; ++i)
        {
            res = (res<<1) + (n&1);
            n >>= 1;
        }
        return res;
}
```

* C++2 (3ms)
```
uint32_t reverseBits(uint32_t n) {
        uint32_t reverse = 0;
        for(int i=0; i<32; i++)
        {
            reverse = (reverse<<1) + n%2;
            n /= 2;
        }
        return reverse;
}
```

* Java1 (3ms)
```
// you need treat n as an unsigned value
    public int reverseBits(int n) {
        int res=0;
        for(int i=0; i<32; ++i)
        {
            res = (res<<1) + n%2;
            n >>>= 1;
        }
        return res;
    }
```

## Explanation

**NOTE :** java has no unsigned integers.

In Java SE 8 and later, you can use the int data type to represent an unsigned 32-bit integer, which has a minimum value of 0 and a maximum value of 2^32-1. Use the Integer class to use int data type as an unsigned integer. Static methods like compareUnsigned, divideUnsigned etc have been added to the Integer class to support the arithmetic operations for unsigned integers.

* **worst-case time complexity:** O(32)
* **worst-case space complexity:** O(1)