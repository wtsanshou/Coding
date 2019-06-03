# WT. Get Modulo

### Wtsanshou

## Question

Modulo two integers without using multiplication, division and mod operator. 

**Note:**

* 0 <= a <= 10<sup>7</sup>
* 0 < b <= 10<sup>7</sup>

**Follow up**

* What if `a=2147483647`?

## Solutions

### Solution 1

* Java 
```
public int modulo(int a, int b){
    if(a < b) return a;
    else if(a == b) return 0;
    else{
        int c = modulo(a, b+b);
        if(c >= b)  c -= b;
        return c;
    }
}
```

Doulbe `b` until it's larger than or equal `a`. In each recurse, is the modulo is  arger than or equal the recursed `b`, minus the recursed `b` from the  modulo.

**Complexity:**

* **worst-case time complexity:** `O(log(a))`.
* **worst-case space complexity:** `O(log(a))`.
