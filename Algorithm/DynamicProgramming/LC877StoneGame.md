# LC877. Stone Game

### LeetCode

## Question

Alex and Lee play a game with piles of stones.  There are an even number of piles arranged in a row, and each pile has a positive integer number of stones piles[i].

The objective of the game is to end with the most stones.  The total number of stones is odd, so there are no ties.

Alex and Lee take turns, with Alex starting first.  Each turn, a player takes the entire pile of stones from either the beginning or the end of the row.  This continues until there are no more piles left, at which point the person with the most stones wins.

Assuming Alex and Lee play optimally, return True if and only if Alex wins the game.

**Example 1:**
```
Input: [5,3,4,5]
Output: true
Explanation: 
Alex starts first, and can only take the first 5 or the last 5.
Say he takes the first 5, so that the row becomes [3, 4, 5].
If Lee takes 3, then the board is [4, 5], and Alex takes 5 to win with 10 points.
If Lee takes the last 5, then the board is [3, 4], and Alex takes 4 to win with 9 points.
This demonstrated that taking the first 5 was a winning move for Alex, so we return true.
``` 

**Note:**

* 2 <= piles.length <= 500
* piles.length is even.
* 1 <= piles[i] <= 500
* sum(piles) is odd.

## Solutions

### Solution 1

* Scala (292 ms, 42.3 MB)
```
def stoneGame(piles: Array[Int]): Boolean = {
    true
}
```

* Java (2 ms, 20.6 MB)
```
public boolean stoneGame(int[] piles) {
    return true;
}
```

The question given that Alex starts first to take the stone, there are even number of piles, and the sum of the stones is odd. This leads to Alex will always win. 

* If `sum(odd piles) > sum(even piles)`, Alex can always take the `odd` piles of stones to get more stones to win.
* If `sum(odd piles) < sum(even piles)`, Alex can always take the `even` piles of stones to get more stones to win.

* **worst-case time complexity:** O(1).
* **worst-case space complexity:** O(1).

### Solution 2

**Follow up**

1. What if the piles.length could be odd as well? Therefore, there is chance for Lee to win.
2. What if we want to know exactly the diffenerce of stones?

* Scala (336 ms, 48 MB)
```
def stoneGame(piles: Array[Int]): Boolean = {
    val n = piles.length
    val dp = Array.ofDim[Int](n, n)
    for {
        i <- 0 until n
        j <- 0 until n
    } if(i == j) dp(i)(j) = piles(i)
    
    for {
        d <- 1 until n  //d is the distance between i and j
        i <- 0 until n-d
    } dp(i)(i+d) = Math.max(piles(i)-dp(i+1)(i+d), piles(i+d)-dp(i)(i+d-1))
    
    dp(0)(n-1) > 0
}
```

Here `dp(i)(j)` `=`the biggest number of stones you can get `minus` the number of stones of the opponent picking piles in `piles(i) ~ piles(j)`.

You can first take `piles(i)` or `piles(j)`

* if you take `piles(i)`, the diffenerce of stones is `piles(i)-dp(i+1)(j)`
* if you take `piles(j)`, the diffenerce of stones is `piles(j)-dp(i)(j-1)`

Then we can get:
```
dp(i)(j) = Math.max(piles(i)-dp(i+1)(j), piles(j)-dp(i)(j-1))
```
We start from smaller subarray and then we use that to calculate the bigger subarray.

Finally, dp(0)(n-1) is the exactly the diffenerce of stones Alex get. If it's bigger than `0`, it means Alex get can get more stons than Lee.

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is the number of the `piles`.
* **worst-case space complexity:** O(n<sup>2</sup>), where `n` is the number of the `piles`.

### Solution 2

**Follow up**
1. Can you use O(n) space?

* Scala (332 ms, 43.7 MB)
```
def stoneGame(piles: Array[Int]): Boolean = {
    val n = piles.length
    val dp = piles.clone // have to use clone, dp=piles will lead both point to the same object
    
    for {
        d <- 1 until n
        i <- 0 until n-d
    } dp(i) = Math.max(piles(i)-dp(i+1), piles(i+d)-dp(i))
    
    dp(0) > 0
}
```

Because the distance is the same when you take `piles(i)` or `piles(j)`. And we start from smaller subarray and then we use that to calculate the bigger subarray. Therefore, we can use a 1-D array to replace the `dp(i)(j)`.

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is the number of the `piles`.
* **worst-case space complexity:** O(n), where `n` is the number of the `piles`.

