# LC464. Can I Win

### LeetCode

## Question

In the "100 game," two players take turns adding, to a running total, any integer from 1..10. The player who first causes the running total to reach or exceed 100 wins.

What if we change the game so that players cannot re-use integers?
For example, two players might take turns drawing from a common pool of numbers of 1..15 without replacement until they reach a total >= 100.

Given an integer maxChoosableInteger and another integer desiredTotal, determine if the first player to move can force a win, assuming both players play optimally.

You can always assume that maxChoosableInteger will not be larger than 20 and desiredTotal will not be larger than 300.

**Example**

**Input:**
```
maxChoosableInteger = 10
desiredTotal = 11
```

**Output:**
```
false
```

**Explanation:**

No matter which integer the first player choose, the first player will lose.
The first player can choose an integer from 1 up to 10.

If the first player choose 1, the second player can only choose integers from 2 up to 10.

The second player will win by choosing 10 and get a total = 11, which is >= desiredTotal.

Same with other integers chosen by the first player, the second player will always win.

## Solutions

* C++1 (126ms)
```
class Solution {
public:
    unordered_map<int, bool> map;
    bool ifWin(int used, int mci, int dt)
    {
        if(dt <= 0) return false;
        if(map.count(used)==0)
        {
            for(int i=0; i<mci; ++i)
            {
                if((1&(used>>i)) == 1)  // ((1<<i) & used) > 0
                {
                    if(!ifWin((1<<i)^used, mci, dt-i-1))
                    {
                        map[used] = true;
                        return true;
                    }
                }
            }
            map[used] = false;
        }
        return map[used];
    }
    bool canIWin(int maxChoosableInteger, int desiredTotal) {
        int sum = maxChoosableInteger * (maxChoosableInteger+1) /2;
        if(sum < desiredTotal) return false;
        if(desiredTotal <= 0) return true;
        int used = (1<<maxChoosableInteger) - 1;
        return ifWin(used, maxChoosableInteger, desiredTotal);
    }
};
```

## Explanation

Because the maxChoosableInteger will not be larger than 20, these choosable integers can be represented by bits of an integer. 

Using backtracking to travel all situations.

* **worst-case time complexity:** O(maxChoosableInteger<sup>2</sup>)
* **worst-case space complexity:** O(maxChoosableInteger<sup>2</sup>)