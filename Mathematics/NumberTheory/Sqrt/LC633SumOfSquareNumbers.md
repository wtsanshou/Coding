# 633. Sum of Square Numbers

### LeetCode

## Question

Given a non-negative integer c, your task is to decide whether there're two integers a and b such that a2 + b2 = c.

**Example 1:**
```
Input: 5
Output: True
Explanation: 1 * 1 + 2 * 2 = 5
```

**Example 2:**
```
Input: 3
Output: False
```

## Solutions

* Java1
```
public boolean judgeSquareSum(int c) {
        int n = (int)Math.sqrt(c);
        for(int a=0; a<=n; ++a){
            int b2 = c - a*a;
            int b = (int)Math.sqrt(b2);
            if(b*b == b2)
                return true;
        }
        return false;
    }
```

## Explanation

**Note :** c is a non-negative integer, be careful the corner case: 
```
0*0 + b*b = c
```

* **worst-case time complexity:** O(log(n))
* **worst-case space complexity:** O(1)

