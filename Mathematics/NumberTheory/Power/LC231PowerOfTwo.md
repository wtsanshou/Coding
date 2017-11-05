# LC231. Power of Two

### LeetCode

## Question

Given an integer, write a function to determine if it is a power of two.

## Solutions

* C++1 (3ms)
```
bool isPowerOfTwo(int n) {
    if(n<=0) return false;
    while(n != 1)
    {
        if(n%2 != 0) return false;
        n /= 2;
    }
    return true;
}
```

* C++2 (3ms)
```
bool isPowerOfTwo(int n) {
    if(n<=0) return false;
    if(n==1) return true;
    return (n%2==0) ? isPowerOfTwo(n/2) : false;
}
```

* C++3 (3ms)
```
bool isPowerOfTwo(int n) {
    return fmod(log10(n)/log10(2), 1) < 1e-15;
}
```

* C++4 (3ms)
```
bool isPowerOfTwo(int n) {
    return n>0 && (n&(n-1))==0;
}
```

* Java1 (3ms)
```
public boolean isPowerOfTwo(int n) {
    return Math.log(n)/Math.log(2) % 1 < 1e-9;
}
```

