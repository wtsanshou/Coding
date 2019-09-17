# Lint653. Expression Add Operators

### LintCode (Hard)

## Question

Given a string that contains only digits 0-9 and a target value, return all possibilities to add binary operators (not unary) +, -, or * between the digits so they evaluate to the target value.

**Example 1:**
```
Input:
"123"
6
Output: 
["1*2*3","1+2+3"]
```

**Example 2:**
```
Input:
"232"
8
Output: 
["2*3+2", "2+3*2"]
```

**Example 3:**
```
Input:
"105"
5
Output:
["1*0+5","10-5"]
```

**Example 4:**
```
Input:
"00"
0
Output:
["0+0", "0-0", "0*0"]
```

**Example 5:**
```
Input:
"3456237490",
9191 
Output: 
[]
```

## Solutions

### Soluiton 1

* Java
```
public class Solution {
    /**
     * @param num: a string contains only digits 0-9
     * @param target: An integer
     * @return: return all possibilities
     */
    public List<String> addOperators(String num, int target) {
        List<String> res = new ArrayList<>();
        dfs(num, 0, target, res, "", 0L, 0L);
        return res;
    }
    
    private void dfs(String num, int start, int target, List<String> res, String one, long possibleVal, long lastVal) {
        if (start == num.length()) {
            if (target == possibleVal) {
                res.add(one);
            }
            return;
        }
        
        for (int i = start; i < num.length(); i++) {
            long val = Long.parseLong(num.substring(start, i + 1));
            
            if (start == 0) {
                dfs(num, i + 1, target, res, "" + val, val, val);
            } else {
                dfs(num, i + 1, target, res, one + "+" + val, possibleVal + val, val);
                dfs(num, i + 1, target, res, one + "-" + val, possibleVal - val, -val);
                dfs(num, i + 1, target, res, one + "*" + val, possibleVal - lastVal + lastVal * val, lastVal * val);
            } 
            if (val == 0) { // get rid of leading 0
                break;
            }
        }
    }
}
```

When I see `return all possibilities`, I know I need to use `DFS`. It's not easy to have the idea of keeping the `lastVal`. And there are some corner cases making this question hard:

1. The individual `val`'s length could be more than 1.
2. For the `*` operation, you need to minus `lastVal` from the `possibleVal` first, and then plus `lastVal * val`.
3. You need to get rid of the leading `0` `val`.
4. The `possibleVal` and `lastVal` could be `long`.
5. Deal with the first individual `val`.

I tried to use `long target` in the `dfs`, but get `Memory Limit Exceede` for the corner case:

```
"000000000000"
0
```

**Complexity:**

* **worst-case time complexity:** Hard to say, maybe O(3<sup>n</sup>), where `n` is the length of the input `num`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input `num`.

