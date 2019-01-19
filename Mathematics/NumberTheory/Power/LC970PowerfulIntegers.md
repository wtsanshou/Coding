# LC970. Powerful Integers

### LeetCode

Given two non-negative integers x and y, an integer is powerful if it is equal to x^i + y^j for some integers i >= 0 and j >= 0.

Return a list of all powerful integers that have value less than or equal to bound.

You may return the answer in any order.  In your answer, each value should occur at most once.

**Example 1:**
```
Input: x = 2, y = 3, bound = 10
Output: [2,3,4,5,7,9,10]
Explanation: 
2 = 2^0 + 3^0
3 = 2^1 + 3^0
4 = 2^0 + 3^1
5 = 2^1 + 3^1
7 = 2^2 + 3^1
9 = 2^3 + 3^0
10 = 2^0 + 3^2
```

**Example 2:**
```
Input: x = 3, y = 5, bound = 15
Output: [2,4,6,8,10,14]
```

**Note:**

* 1 <= x <= 100
* 1 <= y <= 100
* 0 <= bound <= 10^6

## Solutions

* Java1
```
public List<Integer> powerfulIntegers(int x, int y, int bound) {
    Set<Integer> result = new HashSet<>();
    int sqrt = (int)Math.sqrt((double)bound);
    for(int i=0; i<=sqrt; ++i){
        int X = (int)Math.pow(x, i); 
        if(X >= bound) break;
        for(int j=0; j<=sqrt; ++j){
            int Y = (int)Math.pow(y, j); 
            if(Y >= bound) break;
            int powerful = X + Y;
            if(powerful <= bound)
                result.add(powerful);
            if(y == 1) break;
        }
        if(x == 1) break;
    }
    return new ArrayList(result);
}
```

## Explanation

The power will not be larger than the sqrt of the bound.

* **worst-case time complexity:** O(n<sup>2</sup>)
* **worst-case space complexity:** O(n)
