# LC326. Power of Three

### LeetCode

## Question

Given an integer, write a function to determine if it is a power of three.
Follow up: Could you do it without using any loop / recursion?

## Solutions

* C++1 (55ms)
```
bool isPowerOfThree(int n) {
    //return fmod(log10(n)/log10(3),1) <1e-9;
    return fmod(log10(n)/log10(3),1) == 0;
}
```

* C++2 (95ms)
```
bool isPowerOfThree(int n) {
    if(n<1) return false;
    if(n==1) return true;
    while(n>1)
    {
        if(n%3 != 0) return false;
        n /= 3;
    }
    return true;
}
```

* C++3 (49ms)
```
bool isPowerOfThree(int n) {
    if(n<1) return false;
    if(n==1) return true;
    return (n%3 != 0)? false : isPowerOfThree(n/3);
}
```

* Java1 (18ms)
```
public boolean isPowerOfThree(int n) {
    return n>0 && 1162261467%n==0;
}
```

* Java2 (19ms)
```
public boolean isPowerOfThree(int n) {
    if(n==0) return false;
    while(n%3==0) n/=3;
    return n==1;
}
```

## Explanation

**Solution Java1** 3<sup>19</sup> = 1162261467 is the maximum power of three in Integer. Only power of three numbers can be modulared by 3<sup>19</sup> equals 0.
