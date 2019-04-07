# LC517. Super Washing Machines

### LeetCode

## Question

You have n super washing machines on a line. Initially, each washing machine has some dresses or is empty.

For each move, you could choose any m (1 ≤ m ≤ n) washing machines, and pass one dress of each washing machine to one of its adjacent washing machines at the same time .

Given an integer array representing the number of dresses in each washing machine from left to right on the line, you should find the minimum number of moves to make all the washing machines have the same number of dresses. If it is not possible to do it, return -1.

**Example1**
```
Input: [1,0,5]

Output: 3

Explanation: 
1st move:    1     0 <-- 5    =>    1     1     4
2nd move:    1 <-- 1 <-- 4    =>    2     1     3    
3rd move:    2     1 <-- 3    =>    2     2     2   
```

**Example2**
```
Input: [0,3,0]

Output: 2

Explanation: 
1st move:    0 <-- 3     0    =>    1     2     0    
2nd move:    1     2 --> 0    =>    1     1     1     
```

**Example3**
```
Input: [0,2,0]

Output: -1

Explanation: 
It's impossible to make all the three washing machines have the same number of dresses. 
```

**Note:**

1.	The range of n is [1, 10000].
2.	The range of dresses number in a super washing machine is [0, 1e5].

## Solutions

## Solution 1

* C++
```
int findMinMoves(vector<int>& machines) {
    int sum = accumulate(machines.begin(), machines.end(), 0);
    int n = machines.size();
    int ave = sum/n;
    if(ave*n != sum) return -1; //if(sum%ave != 0) return -1;
    int res = 0, steps=0;
    for(int m : machines)
    {
        steps += m - ave;
        res = max(res, max(m-ave, abs(steps)));
    }
    return res;
}
```

Because we could choose any m (1 ≤ m ≤ n) washing machines.

Imaging the the number of dresses as a list of hills and pits.

```
 *
 *       *
**       *
**  **  **
*** ** ***
3510220124
```

The minimum number of moves will be affected only by the most highest hills group or the most lowest pits group.

* **worst-case time complexity:** `O(n)`, where `n` is the number of the `machines`.
* **worst-case space complexity:** `O(1)`
