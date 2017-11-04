# LC70. Climbing Stairs

### LeetCode

## Question

You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

**Note:** Given n will be a positive integer.

## Solutions

* C++1 (0ms)
```
int climbStairs(int n) {
    if(n<2) return 1;
    int f1=1, f2=1, res=0;
    for(int i=2;i<=n;i++)
    {
        res = f1+f2;
        f1=f2;
        f2=res;
    }
    return res;
}
```

* Java1 (TLE)
```
public int climbStairs(int n) {
    if(n<2) return 1;
    else if(n==2) return 2;
    else return climbStairs(n-1) + climbStairs(n-2);
}
```

## Explanation

Recursive method is easier to understand and save some lines of code, but will consume a lot of duplicated calculation.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)