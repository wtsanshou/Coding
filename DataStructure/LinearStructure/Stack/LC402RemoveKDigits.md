# LC402. Remove K Digits

### LeetCode

## Question

Given a non-negative integer num represented as a string, remove k digits from the number so that the new number is the smallest possible.

**Note:**

* The length of num is less than 10002 and will be ≥ k.
* The given num does not contain any leading zero.

**Example 1:**
```
Input: num = "1432219", k = 3
Output: "1219"
Explanation: Remove the three digits 4, 3, and 2 to form the new number 1219 which is the smallest.
```

**Example 2:**
```
Input: num = "10200", k = 1
Output: "200"
Explanation: Remove the leading 1 and the number is 200. Note that the output must not contain leading zeroes.
```

**Example 3:**
```
Input: num = "10", k = 2
Output: "0"
Explanation: Remove all the digits from the number and it is left with nothing which is 0.
```

## Solutions

* C++1
```
string removeKdigits(string num, int k) {
    int size=num.length();
    int digitS = size-k;
    char sta[size];
    int i=0, top=-1;
    for(; i<size; ++i)
    {
        while(top>-1 && sta[top]>num[i] && k>0)
        {
            top--;
            k--;
        }
        sta[++top] = num[i];
    }
    int start=0;
    while(start<digitS && sta[start]=='0') //check start position first
        start++;
    return start==digitS ? "0" : string(sta, start, digitS-start);
}
```

## Explanation

Traverse the string `num` from left-hand to right-hand digits. 

Using a `stack` to remember the left-hand digits. when found a smaller digits than the digits in the `stack`, `pop` them from the `stack` until `k` digits.

The rest digits are the result.

* **worst-case time complexity:** O(N), where `N` is the length of the input string `num`.
* **worst-case space complexity:** O(N), where `N` is the length of the input string `num`.