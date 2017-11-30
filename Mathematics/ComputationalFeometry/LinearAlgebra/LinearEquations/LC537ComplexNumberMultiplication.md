# LC537. Complex Number Multiplication

### LeetCode

## Question

Given two strings representing two complex numbers.

You need to return a string representing their multiplication. Note i<sup>2</sup> = -1 according to the definition.

**Example 1:**

```
Input: "1+1i", "1+1i"
Output: "0+2i"
```

**Explanation: **

(1 + i) * (1 + i) = 1 + i<sup>2</sup> + 2 * i = 2i, and you need convert it to the form of 0+2i.

**Example 2:**

```
Input: "1+-1i", "1+-1i"
Output: "0+-2i"
```

**Explanation:** 

(1 - i) * (1 - i) = 1 + i<sup>2</sup> - 2 * i = -2i, and you need convert it to the form of 0+-2i.

Note:

* The input strings will not have extra blank.
* The input strings will be given in the form of a+bi, where the integer a and b will both belong to the range of [-100, 100]. And the output should be also in this form.

## Solutions

* C++1 (3ms)
```
class Solution {
public:
    vector<int> getNums(string s)
    {
        int i=0;
        vector<int> res(2);
        while(s[i]!='+') ++i;
        res[0] = stoi(s.substr(0, i));
        res[1] = stoi(s.substr(i+1, s.length()-1));
        return res;
    }
    string complexNumberMultiply(string a, string b) {
        vector<int> A = getNums(a);
        vector<int> B = getNums(b);
        return to_string(A[0]*B[0] - A[1]*B[1]) + "+" + to_string(A[0]*B[1] + A[1]*B[0]) + "i";
    }
};
```

* C++2
```
vector<int> getNums(string s)
{
    int i=0;
    while(s[i]!='+') ++i;
    int x = stoi(s.substr(0, i));
    int y = stoi(s.substr(i+1, s.length()-1));
    return vector<int> ({x, y});
}
```

## Explanation

1. Get the values of the two complex numbers.
2. (A+Bi) * (C+Di) = (A*C - B*D) + (A*D + B*C) i.

* **worst-case time complexity:** O(len(a) + len(b))
* **worst-case space complexity:** O(1)