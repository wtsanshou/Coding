# LC50. Pow(x, n)

### LeetCode

## Question

Implement `pow(x, n)`.

## Solutions

* C++1
```
double myPow(double x, int n) {
    if(n == 0)
        return 1;
    if(n<0){
        if(n == INT_MIN) return (1/x)*myPow(x, n+1);
        n = -n; //or return myPow(1/x, -n)
        x = 1/x;
    }
    return (n%2 == 0) ? myPow(x*x, n/2) : x*myPow(x*x, n/2);
}
```

* C++2
```
double myPow(double x, int n) {
    x = (n>0) ? x:1/x;
    double res=1;
    for(double temp=x; n!=0; n/=2)
    {
        if (n%2!=0) res*=temp;
        temp*=temp;
    }
    return res;
}
```

* C++3
```
double myPow(double x, int n) {
    if(n==0) return 1;
    double t = myPow(x, n/2);
    return (n%2==0 ? 1 : ((n<0)? 1/x : x)) * t*t;
}
```

## Explanation

A corner case is n == `-2147483648`. If we try to remove the minus sign, the number `2147483648` would overflow the maximum value of Integer.

Solutions 2 and 3 solved the problem.

* **worst-case time complexity:** O(log(n))
* **worst-case space complexity:** O(1)



