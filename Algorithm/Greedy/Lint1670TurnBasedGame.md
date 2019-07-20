# Lint1670. Turn-Based Game

### LintCode

## Question

QW is a player of a turn-based game, and today he decided to kill monsters.

QW will fight with n monsters in a battle. Each monster has an attack power atk[i]. If the i-th monster is still alive at the end of each round, it will cause atk[i] damage to the QW. QW can only kill one monster at the beginning of each round. Please calculate how much damage he needs to suffer at least after QW kill all the monsters.

**Example 1:**
```
Input: 
atk = [19,3]

Output: 
3
```

**Example 2:**
```
Input: 
atk = [1,3,2,5]

Output: 
10
```

**Notice**

* n, atk[i] <= 100000
* The answer may exceed the range of int

## Solutions

### Solution 1

* Java
```
public long getAns(int[] atk) {
    long sum = 0;
    for (int value : atk)
        sum += value;
    
    Arrays.sort(atk);
    
    long res = 0;
    for (int i = atk.length-1; i > 0; i--) {
        sum -= atk[i];
        res += sum;
    }
        
    return res;
}
```

This is not a difficult quesiton. If you have ever played game, it's very obvious that we just need to kell the most damage monster in each round. The damage to QW in each round will be the sum of the rest monsters' damage.

So, we just need to sum the damage of all monsters at the beginning. Then in each round mins the most damage monster from the sum.

**NOTE** The sum and the result could be execced interge range.

**Complexity:**

* **worst-case time complexity:** `O(n * log(n))`, where `n` is the length of the input `atk`.
* **worst-case space complexity:** `O(log(n))`, where `n` is the length of the input `atk`.

