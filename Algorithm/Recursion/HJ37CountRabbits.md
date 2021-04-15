# HJ37. Count Rabbits

### NowCoder

## Question

A rabbit need 3 months to grow up. After grow up a rabbit can born 1 rabbit every month. Suppose the rabbits will never die, you have 1 rabbit at 0 month. Your task is to count the number of rabbits you have at month `n`?

**Example:**
```
Input: 9
Output: 34
```

**Note:**
1. `n` will not exceed 40.


## Solutions

### Solution 1

* Java
```
public int countRabbits(int n) {
    if (n < 3) {
        return 1;
    }
    int res = 1;
    for (int i = n - 2; i > 0; i--) {
        res += countRabbits(i);
    }
    return res;
}
```

```
            1
           /
          /
         /\
        1  1 countRabbits(n - 3)
       / \
      1   1  countRabbits(n - 4)
     / \           .
    ..  ..         . 
```

countRabbits(n) = 1 + countRabbits(n - 3) + countRabbits(n - 4) + ... + countRabbits(1)

**Complexity:**

* **worst-case time complexity:** O(2<sup>n</sup>), where `n` is the number of month `n`.
* **worst-case space complexity:** O(2<sup>n</sup>), where `n` is the number of month `n`.
