# Lint1668. Interval Minimum Coverage

### LintCode

## Question

There are n intervals in number axis. Now we need to choose some points to make that there is at least one point in each interval.

Return the minimum number of chosen points.

**Example 1:**

```
Input: 
[(1,5), (4,8), (10,12)]

Output: 
2

Explanation: 
  Choose two points: 5, 10
  The first  interval [1, 5] contains 5
  The second interval [4, 8] contains 5
  The third  interval [10, 12] contains 10
```

**Example 2:**
```
Input: 
[(1,5), (4,8), (5,12)]

Output: 
1

Explanation: 
All intervals contain 5
```

**Notice**

* 1 <= n <= 10^4
* We guarantee that the given intervals are valid and the left and right endpoints of each interval are within the range of [0, 10 ^ 5].
* They are closed intervals.

## Solutions

### Solution 1

* java
```
public int getAns(List<Interval> a) {
    Collections.sort(a, (x, y) -> Integer.compare(x.start, y.start));
    
    int res = 1;
    Interval minInterval = a.get(0);
    
    for (int i = 1; i < a.size(); i++) {
        Interval cur = a.get(i);
        if (cur.start > minInterval.end) {
            res++;
            minInterval = cur;
        } else {
            minInterval.start = Math.max(minInterval.start, cur.start);
            minInterval.end = Math.min(minInterval.end, cur.end);
        }
    }
    
    return res;
}
```

At the beginning, I thought this question is asking the number of group of connected intervals. Then based on an test case:

```
Input: 
[(1,5), (4,8), (10,12), (9,9), (9,10)]

Output: 
3

Explanation: 
  Choose two points: 5, 10
  The first  interval [1, 5] contains 5
  The second interval [4, 8] contains 5
  The third  interval [10, 12] contains 10
  The fourth  interval [9, 9] contains 9
  The fifth  interval [9, 10] contains 9
```

I realize the question is asking for the minimum number of points which make that there is at least one point in each interval. This make me remember a LeetCode question **LC554. Brick Wall** which asked to draw a vertical line from the top to the bottom and cross the least bricks. It's not using greedy algorthm, but it helps me to draw my thought.

So the solution is to greedy algorithm. Always update the minimum common interval of a group of intervals. When found an interval is outside of the common interval, there must be one more vertical line from the top to the bottom, and update a new minimum common interval. 

**Complexity:**

* **worst-case time complexity:** `O(n * log(n))`, where `n` is the length of the input `a`.
* **worst-case space complexity:** `O(log(n))`, where `n` is the length of the input `a`.
