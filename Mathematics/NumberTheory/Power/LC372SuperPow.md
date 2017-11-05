# LC372. Super Pow

### LeetCode

## Question

Your task is to calculate a<sup>b</sup> mod 1337 where a is a positive integer and b is an extremely large positive integer given in the form of an array.

**Example1:**
```
a = 2
b = [3]

Result: 8
```

**Example2:**

```
a = 2
b = [1,0]

Result: 1024
```

## Solutions

* C++1
```
class Solution {
    int base = 1337;
public:
    int Pow(int a, int n)
    {
        a %= base;
        int res = 1;
        for(int i=0; i<n; ++i)
            res = (res*a) % base;
        return res;
    }
    int superPow(int a, vector<int>& b) {
        if(b.empty()) return 1;
        int digit = b.back();
        b.pop_back();
        return (Pow(superPow(a, b), 10) * Pow(a, digit)) % base;
    }
};
```

## Explanation

1. a<sup>x+y</sup> % base == (a<sup>x</sup> % base) * (a<sup>y</sup> % base)
2. a<sup>x</sup> % base == (a % base)<sup>x</sup> % base 





