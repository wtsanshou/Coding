# Lint1538. Card Game II

### LintCode

## Question

You are playing a card game with your friends, there are n cards in total. Each card costs cost[i] and inflicts damage[i] damage to the opponent. You have a total of totalMoney dollars and need to inflict at least totalDamage damage to win. And Each card can only be used once. Determine if you can win the game.

**Example 1**
```
Input:
cost = [1,2,3,4,5]
damage = [1,2,3,4,5]
totalMoney = 10
totalDamage = 10

Output: 
true

Explanation: 
We can use the [1,4,5] to cause 10 damage, which costs 10.
```

**Example 2**
```
Input:
cost = [1,2]
damage = [3,4]
totalMoney = 10
totalDamage = 10

Output: 
false

Explanation: 
We can only cause 7 damage at most.
```

## Solutions

### Solution 1

* Java
```
public class Solution {
    /**
     * @param cost: costs of all cards
     * @param damage: damage of all cards
     * @param totalMoney: total of money
     * @param totalDamage: the damage you need to inflict
     * @return: Determine if you can win the game
     */
    public boolean cardGame(int[] cost, int[] damage, int totalMoney, int totalDamage) {
        return dfs(cost, 0, damage, totalMoney, totalDamage);
    }
    
    private boolean dfs(int[] cost, int start, int[] damage, int totalMoney, int totalDamage) {
        if (start >= cost.length) {
            if (totalDamage <= 0 && totalMoney >= 0) return true;
            return false;
        }
        
        boolean win = false;
        
        for (int i = start; i < cost.length; i++) {
            if (cost[i] > totalMoney) continue;
            if (damage[i] >= totalDamage) return true;
            win = win || dfs(cost, i + 1, damage, totalMoney - cost[i], totalDamage - damage[i]);
        }
        
        return win;
    }
}
```

At the beginning, I was thinking to sort the `cost` and `damage` by `damage / cost` or `cost / damage` rate. But then I realize with the limitation of `totalMoney`, the rate is not useful.

I feel it could be solved by brute force, but I think it may be too slow.

Finally, I had no time. So I came back to brute force solution. The idea is to use `DFS` starting from each card. 

Should be solved by `Memory search`

**Exit Points**

1. `start >= cost.length`, all cards have been visited. If you can win at this point (`totalDamage <= 0 && totalMoney >= 0`), return true, else return false.
2. `damage[i] >= totalDamage`, it means found a soltion to win.

**Complexity:**

* **worst-case time complexity:** O(2<sup>n</sup>), where `n` is the length of the input `cost`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input `cost`.

### Solution 2

Then, I was thinking to use `DP`, here is the code:

* Java
```
public  boolean cardGame(int[] cost, int[] damage, int totalMoney, int totalDamage) {
    int[][] dp = new int[cost.length + 1][totalMoney + 1];
    for (int i = 1; i < cost.length; i++) {
        for (int j = cost[i]; j <= totalMoney; j++) {
            dp[i][j] = Math.max(dp[i - 1][j], dp[i - 1][j - cost[i]] + damage[i]);
            if (dp[i][j] >= totalDamage)
                return true;
        }
    }
    return false;
}
```

**State**

`dp[i][j]` is the the maximum damage with the first `i` cards and `j` totalMoney.

**Function**

`dp[i][j] = Math.max(dp[i - 1][j], dp[i - 1][j - cost[i]] + damage[i])`

**Initialization**

`dp[i][j] = 0`

**Result**

`any (dp[i][j] >= totalDamage)`


**Complexity:**

* **worst-case time complexity:** `O(n * m)`, where `n` is the length of the input `cost`, `m` is the `totalMoney`.
* **worst-case space complexity:** `O(n * m)`, where `n` is the length of the input `cost`, `m` is the `totalMoney`.

### Solution 3

* Java (Roll Optimize)
```
public static boolean cardGame(int[] cost, int[] damage, int totalMoney, int totalDamage) {
    int[][] dp = new int[2][totalMoney + 1];
    for (int i = 1; i < cost.length; i++) {
        for (int j = cost[i]; j <= totalMoney; j++) {
            dp[i % 2][j] = Math.max(dp[(i - 1) % 2][j], dp[(i - 1) % 2][j - cost[i]] + damage[i]);
            if (dp[i % 2][j] >= totalDamage)
                return true;
        }
    }
    return false;
}
```

**Complexity:**

* **worst-case time complexity:** `O(n * m)`, where `n` is the length of the input `cost`, `m` is the `totalMoney`.
* **worst-case space complexity:** `O(m)`, where `m` is the `totalMoney`.

### Solution 4 (Finite Packpack)

* Java
```
public boolean cardGame(int[] cost, int[] damage, int totalMoney, int totalDamage) {
    int[] dp = new int[totalMoney + 1];

    for (int i = 1; i < cost.length; i++) {
        for (int money = totalMoney; money >= cost[i]; money--) {
            dp[money] = Math.max(dp[money], dp[money - cost[i]] + damage[i]);
            if (dp[money] >= totalDamage)
                return true;
        }
    }

    return false;
}
```

For finite number of elements in the backpack, loop from big value (`totalMoney`) to small value (`cost[i]`). Or use another dimension to indicate the number of card.

**Complexity:**

* **worst-case time complexity:** `O(n * m)`, where `n` is the length of the input `cost`, `m` is the `totalMoney`.
* **worst-case space complexity:** `O(m)`, where `m` is the `totalMoney`.
