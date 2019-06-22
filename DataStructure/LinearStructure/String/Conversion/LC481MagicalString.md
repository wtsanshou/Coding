# LC481. Magical String

### LeetCode

## Question

A magical string S consists of only '1' and '2' and obeys the following rules:
The string S is magical because concatenating the number of contiguous occurrences of characters '1' and '2' generates the string Sitself.

The first few elements of string S is the following: S = `"1221121221221121122……"`

If we group the consecutive '1's and '2's in S, it will be:
`1 22 11 2 1 22 1 22 11 2 11 22 ......`

and the occurrences of '1's or '2's in each group are:
`1 2 2 1 1 2 1 2 2 1 2 2 ......`

You can see that the occurrence sequence above is the S itself.

Given an integer N as input, return the number of '1's in the first N number in the magical string S.

**Note:** N will not exceed 100,000.

**Example 1:**

```
Input: 6
Output: 3
Explanation: The first 6 elements of magical string S is "122112" and it contains three 1's, so return 3.
```

## Solutions

### Solution 1

* C++ (9ms)
```
int magicalString(int n) {
    if(n==0) return 0;
    queue<int> q;
    q.push(2);
    int res = 1;
    for(int i=2; i<n; ++i)
    {
        int repeat = q.front();
        q.pop(); //remove a front element from the queue
        if(repeat==1) res++;
        int input = q.back() ^ 3;
        for(int j=0; j<repeat; ++j)
            q.push(input);
    }
    return res;
}
```

**Note** `1` and `2` groups appear alternately.

**For example**

```
1 22 11 2 1 22 1 22 11 2 11 22 ......
```

`q.back() ^ 3` will give you an alternately number between `1` and `2`.

`q.front()` is the repeat times. Pop it in each turn.

So, simulate the `Magical String` generation process n turns. Durning this simulation, count the `1` at the font of the queue in each turn.

**Complexity:**

* **worst-case time complexity:** `O(n)`
* **worst-case space complexity:** `O(n)`.

### Solution 2

* C++
```
int magicalString(int n) {
    string S = "122";
    int i = 2;
    while (S.size() < n)
        S += string(S[i++] - '0', S.back() ^ 3);
    return count(S.begin(), S.begin() + n, '1');
}
```

Using `i` to remember the index of repeat times in each turn. Generate the `Magical String`.

Finally count `1` in the substring with size `n` in the generated `Magical String` `S`.

**Complexity:**

* **worst-case time complexity:** `O(n)`
* **worst-case space complexity:** `O(n)`.

### Solution 3

* Java (10ms)
```
class Solution {
    
    private static List<Integer> S = new ArrayList<>();
    private static List<Integer> res = new ArrayList<>();
    private static int i = 2;
    
    static{
        S.add(1);
        S.add(2);
        S.add(2);
        res.add(1);
        res.add(1);
        res.add(1);
    }

    public int magicalString(int n) {
        while (res.size() < n){
            int times = S.get(i++);
            int val = S.get(S.size()-1) ^ 3;
            for(int i=0; i<times; i++){
                S.add(val);
                int previousOne = res.get(res.size()-1);
                res.add(val==1 ? previousOne+1 : previousOne);
            }
        }
        return n==0 ? 0 : res.get(n-1);
    }
}
```

I am trying to use static List to remember the result from 1 to n. So that we don't need to recalculate the small numbers. But the runtime does not reduce, it may means the test case size is not big.

**Complexity:**

* **worst-case time complexity:** `O(n)`
* **worst-case space complexity:** `O(n)`.
