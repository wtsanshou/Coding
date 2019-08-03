# Lint1683. Kill Monster

### LintCode

## Question

There are n monsters and an Altman. Both Altman and Monster have five attribute values. When Altman's five attributes are greater than or equal to the five attributes of a monster, Altman can kill the monster. When Altman kills a monster, the five properties of the monster are added to Altman. How many monsters can Altman kill at most?

**Example 1:**
```
Input: 
n = 2, v = [[1,1,1,1,1],[1,1,1,1,1],[2,2,2,2,2]]

Output: 
2

Explanation: 
Altman kills monster v[1] at first, and his attribute changes to [2,2,2,2,2]. Then Altman can kill monster v[2]
```

**Example 2:**
```
Input: 
n = 5, v = [[3,9,2,1,5],[0,9,6,5,9],[6,1,8,6,3],[3,7,0,4,4],[9,9,0,6,5],[5,6,5,6,7]]

Output: 
0

Explanation: 
Altman can not kill any monster.
```

**Notice**

* v[0][0]-v[0][4] means the 5 values of ALtman. v[1]-v[n] means n monsters' 5 value5.

## Solutions

### Solution 1

* Java
```
public class Solution {

    public int killMonster(int n, int[][] v) {
        List<List<Integer>> monsters = new LinkedList<>();
        for (int i = 1; i < v.length; i++) {
            List<Integer> monster = new ArrayList<>(5);
            for (int j = 0; j < 5; j++)
                monster.add(v[i][j]);
            monsters.add(monster);
        }
        int res  = 0;
        boolean canKill = true;
        while (canKill) {
            canKill = false;
            Iterator it = monsters.iterator();
            while (it.hasNext()) {
                List<Integer> curMonster = (List<Integer>)it.next();
                if (kill(v[0], curMonster)) {
                    add(v[0], curMonster);
                    it.remove();
                    canKill = true;
                    res++;
                }
            }
        }
        
        return res;
    }
    
    private boolean kill(int[] altman, List<Integer> monster) {
        for (int i = 0; i < 5; i++)
            if (altman[i] < monster.get(i))
                return false;
        return true;
    }
    
    private void add(int[] altman, List<Integer> monster) {
        for (int i = 0; i < 5; i++)
            altman[i] +=  monster.get(i);
    }
}
```

At the beginning, I was thinking to sort the monsters. But there are 5 attribute values for each monster, cannot decide to sort by which attribute. So sorting is not a solution.

To solve it, I decide to use brute force. I just check all the rest monsters, if `Altman` can kill it, remove it from the rest monsters. Repeat the process untill no monster can be killed.

**NOTE** in Java, you have to use iterator to remove element from List during loopping it.

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>), where `n` is the length of the input `v`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input `v`.


