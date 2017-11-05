# LC342. Power of Four

### LeetCode

## Question

Given an integer (signed 32 bits), write a function to check whether it is a power of 4.

**Examples: **

```
Given num = 16, 
return true. 
```

```
Given num = 5, 
return false.
```

**Follow up:** Could you solve it without loops/recursion?

## Solutions

* C++1 (3ms)
```
bool isPowerOfFour(int num) {
    return fmod(log10(num)/log10(4), 1) < 1e-16;
}
```

* C++2 (8ms)
```
bool isPowerOfFour(int num) {
    return !(num&(num-1)) && !((num-1)%3);
}
```

* C++3 (8ms)
```
bool isPowerOfFour(int num) {
    return !(num&(num-1)) && (num & 0x55555555);
}
```

* C++4 (3ms)
```
bool isPowerOfFour(int num) {
    if(num<=0) return false;
    while(num > 1)
    {
        if(num%4 != 0) return false;
        num /= 4;
    }
    return num == 1;
}
```

* Java 1 (2ms)
```
public boolean isPowerOfFour(int num) {
    return (Math.log10(num)/Math.log10(4))%1 < 1e-9;
}
```

* Java2 (22ms)
```
public boolean isPowerOfFour(int num) {
    return Integer.toString(num, 4).matches("10*");
}
```

## Explanation

**Solution C++3** `!(num&(num-1))` is power of two. `0x55555555` is `0101 0101 0101 0101 0101 0101 0101 0101`. If `(num & 0x55555555)` is not `0`, the `num` could be a `1` at any position in the bits `0x55555555` which is power of four.

**Solution Java2** `Integer.toString(num, 4)` convert `num` to quaternary string. Regex `10*` means zero or more times of `0`.

