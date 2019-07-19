# Lint1667. Interval Statistics

### LintCode

## Question

Given arr, an array of 01 and an integer k. You need to count how many intervals meet the following conditions:

Both start and the end of the interval are 0 (allowing the length of the interval to be 1).
The number of 1 in the interval is not more than k

**Example 1:**
```
Input: 
arr = [0, 0, 1, 0, 1, 1, 0], k = 1

Output: 
7

Explanation: 
[0, 0], [1, 1], [3, 3], [6, 6], [0, 1], [0, 3], [1, 3] (The interval [i, j] means the elements between index i(included) and index j(included))
```

**Example 2:**
```
Input: 
arr = [1, 1, 1, 0, 0, 1], k = 2

Output: 
3

Explanation: 
[3, 3], [4, 4], [3, 4] (The interval [i, j] means the elements between index i(included) and index j(included))
```

**Notice**

* The length of arr does not exceed 10<sup>5</sup>

## Solutions

### Solution 1

* Java (1258ms) (StackOverflowException)
```
public class Solution {
    /**
     * @param arr: the 01 array
     * @param k: the limit 
     * @return: the sum of the interval
     */
    public long intervalStatistics(int[] arr, int k) {
        int res = 0;
        for (int i = 0; i < arr.length; i++) {
            if(arr[i] == 0)
                res += trackingStartFrom(arr, k, i, 0);
        }
        return res;
    }
    
    private int trackingStartFrom(int[] arr, int k, int start, int sum) {
        if (start >= arr.length || sum > k) return 0;
        
        int res = 0;
        if (arr[start] == 0) 
            res += trackingStartFrom(arr, k, start + 1, sum) + 1;
        else if (sum < k)
            res += trackingStartFrom(arr, k, start + 1, sum + 1);
        
        return res;
    }
}
```

* refactor `trackingStartFrom`
```
private int trackingStartFrom(int[] arr, int k, int start, int sum) {
    if (start >= arr.length) return 0;
    
    if (arr[start] == 0) 
        return trackingStartFrom(arr, k, start + 1, sum) + 1;
    else if (sum < k)
        return trackingStartFrom(arr, k, start + 1, sum + 1);
    
    return 0;
}
```

When I see a question asking for `how many possible combination?`, my first reaction is it may need to use recursive, back tracking, or DP. 

Starting from the recursive solution, the sub solution must be starting from `0`, so I can use a for loop to start the sub solution `trackingStartFrom` starting from each `0`. I was planing to put the for loop into the sub solution, but later I found the sub solution does not need for loop again, because the interval must be continuous. So I moved the for loop out of the sub solution. 

In the sub solution `trackingStartFrom`, where `start` is the starting check point of the sub solution, `sum` is the sum of `1` in the window. The exit point is when the `start` move to outside of the `arr`. The result of the sub solution is coming from `3` cases:

1. If `arr[start] == 0` => 1 plus its sub solution starting from `start + 1` with the same `sum`.
2. If `arr[start] != 0 && sum < k` => its sub solution starting from `start + 1` with the `sum + 1`. 
3. If `arr[start] != 0 && sum >= k` => there is no solution, so return `0`.

This solution is very nice and elegant, but it's stack overflowed. Because the length of arr could be 10<sup>5</sup>, recursive cannot reach that deep.

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is length of `arr`.
* **worst-case space complexity:** `O(n)`, where `n` is length of `arr`.

### Solution 2

* Java (3300 ms) (Time Limit Exceeded)
```
public long intervalStatistics(int[] arr, int k) {
    int res = 0;
    int n = arr.length;
    
    for (int i = 0; i < n; i++) {
        if (arr[i] == 0) {
            for (int j = i, sum = 0; j < n && sum <= k; j++) {
                if (arr[j] == 0)
                    res++;
                else
                    sum++;
            }
        }
    }
    
    return res;
}
```

Base on the `StackOverflowException` of **Solution 1**, I have to use iteration instead of recursion. At first, I was thinking to use DP, but I found I may need n<sup>2</sup> space. If `n` reach to 10<sup>5</sup>, it must be space limit exceeded. So that I gived up DP solution.

Then, I just use iteration (a for loop) to implement the sub solution `trackingStartFrom` in **Solution 1**.

However, it's `Time Limit Exceeded` this time!

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is length of `arr`.
* **worst-case space complexity:** `O(1)`.

### Solution 3

* Java (638 ms)
```
public long intervalStatistics(int[] arr, int k) {
    long res = 0;
    int n = arr.length;
    
    for (int i = 0; i < n; i++) {
        if (arr[i] == 0) {
            long count = 0;
            boolean firstOne = true;
            int jump = i;
            int j = i;
            for (int sum = 0; j < n && sum <= k; j++) {
                if (arr[j] == 0)
                    count++;
                else {
                    sum++;
                    if (firstOne) {
                        firstOne = false;
                        jump = j;
                    }
                }
            }
            long zeroAfterOne = count - jump + i;
            long intervalsAfterOne = (jump == i) ? 0 : (zeroAfterOne * (zeroAfterOne + 1) / 2);
            res += (count * (count + 1) / 2) - intervalsAfterOne;
            i = jump == i ? j : jump;
        }
    }
    
    return res;
}
```

Base on the `Time Limit Exceeded` of **Solution 2**, I have to optimize it. I don't think the outside for loop can be optimized. So I focus on the inside for loop. 

How can reduce `O(n)` to `O(log(n))` or `O(1)`? 

I found there is a chance to let `i` to skip continuous `0`.

I drawed a picture of an example

```
Input:
Index   0, 1, 2, 3, 4, 5, 6    
Value   0, 0, 1, 0, 0, 1, 0    
        ------------|           4
           ---------|           3
                 ---|           2
                   -|           1
                 ---------|     3
                    ------|     2
                         -|     1

Output:                 13
```

I found the number of solution of an window is sum of 1 to the number of `0` in it. But here I cannot jump to index `4`, because the values in index `3` and `4` can be combined with the value in index `6`. It's safe to jump to index `2` or `3` (in other word, the index of the first `1` in the window), because the values in index `0` and `1` will never be used anymore.

So it's safe to add number of intervals starting from index `0` and `1`. It can be calculated by `(count * (count + 1) / 2) - (zeroAfterOne * (zeroAfterOne + 1) / 2)`, where `count` is the number of `0` in the window, `zeroAfterOne` the number of `0` after the first `1` in the window.

**NOTE** a corner case is that there is no `1` in the window, in this case we can skip the whole window.

**Example 3**
```
input: 
10,000 `0`, k=80,000

output: 
4999950000
```

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is length of `arr`.
* **worst-case space complexity:** `O(1)`.

