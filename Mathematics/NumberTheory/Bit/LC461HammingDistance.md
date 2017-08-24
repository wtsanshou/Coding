# LC461. Hamming Distance

### LeetCode

## Question

The Hamming distance between two integers is the number of positions at which the corresponding bits are different.

Given two integers x and y, calculate the Hamming distance.

**Note:**

0 ≤ x, y < 2<sup>31</sup>.

**Example:**

Input: x = 1, y = 4

Output: 2

**Explanation:**
```
1   (0 0 0 1)
4   (0 1 0 0)
       ↑   ↑
```

The above arrows point to positions where the corresponding bits are different.

## Solution

* C++1 (6ms) O(1)
```
int hammingDistance(int x, int y) {
    int res = 0;
    while(x>0 || y>0)
    {
        res += (x & 1) ^ (y & 1);
        x>>=1;
        y>>=1;
    }
    return res;
}
```

* Python 1
```
def hammingDistance(self, x, y):
    return bin(x^y).count('1')
```

## Explanation

`0 ^ 1 = 1`, `1 ^ 0 = 1`

Count the number of the above

* **worst-case time complexity:** O(32)
* **worst-case space complexity:** O(1)
