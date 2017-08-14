# LC441. Arranging Coins

### LeetCode

## Question

You have a total of n coins that you want to form in a staircase shape, where every k-th row must have exactly k coins.

Given n, find the total number of full staircase rows that can be formed.
n is a non-negative integer and fits within the range of a 32-bit signed integer.

## Solutions

* C++1 (15ms)
```int arrangeCoins(int n) {
        long coin = sqrt(n);
        while((coin*(coin+1))/2 <=n)
            coin++;
        return coin-1;
}
```

* C++2 (12ms)
```int arrangeCoins(int n) {
        long layer = sqrt(2*(long)n);
        int sum = (layer * (layer+1)) / 2;
        return (sum > n) ? layer-1 : layer;
}
```

* C++3 (9ms)
```int arrangeCoins(int n) {
        long sum = 2*(long)n;
        long layer = sqrt(sum);
        long res = (layer * (layer+1))/2;
        return (res > n) ? layer-1 : layer;
}
```

* C++4 (9ms)
```
1+2+3+...+x = n
-> (1+x)x/2 = n
-> x^2+x = 2n
-> x^2+x+1/4 = 2n +1/4
-> (x+1/2)^2 = 2n +1/4
-> (x+0.5) = sqrt(2n+0.25)
-> x = -0.5 + sqrt(2n+0.25)
```

```
int arrangeCoins(int n) {
     return floor(-0.5+sqrt((double)2*n+0.25));
}
```

* C++5 (log(n))
```int arrangeCoins(int n) {
        long low = 1, high = n;
        while (low < high) {
            long mid = low + (high - low + 1) / 2;
            if ((mid + 1) * mid / 2.0 <= n) low = mid;
            else high = mid - 1;
        }
        return high;
    }
```

## Explanation

1. Calculate the layer number of `sum>n`. O(log(n))
2. Calculate how many layer could be made by n. O(1)
3. O(1)
4. O(1)
5. Binary search O(log(n))

* **worst-case space complexity:** O(1)
