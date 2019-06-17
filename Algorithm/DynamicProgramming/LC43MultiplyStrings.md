# LC43. Multiply Strings

### LeetCode

## Question

Given two non-negative integers num1 and num2 represented as strings, return the product of num1 and num2.

**Note:**

1.	The length of both num1 and num2 is < 110.
2.	Both num1 and num2 contains only digits 0-9.
3.	Both num1 and num2 does not contain any leading zero.
4.	You must not use any built-in BigInteger library or convert the inputs to integer directly.

## Solutions

### Solution 1

* C++
```
class Solution {
public:
    string multiplyOneDigit(string num2, int n)
    {
        string res = "";
        int carry=0;
        for(int i=num2.length()-1; i>=0; --i)
        {
            int a =num2[i]-'0';
            int mult = a*n +carry;
            carry = mult/10;
            res += to_string(mult%10);
        }
        return carry>0 ? res + to_string(carry) : res;
    }
    string add(string pre, string cur, int len)
    {
        string res = pre.substr(0, len);
        int i=len, j=0, carry=0;
        int pLen= pre.length(), cLen = cur.length();
        while(i<pLen || j<cLen || carry>0)
        {
            int a = i<pLen ? pre[i++]-'0' : 0;
            int b = j<cLen ? cur[j++]-'0' : 0;
            int sum = a+b+carry;
            carry = sum/10;
            res += to_string(sum%10);
        }
        return res;
    }
    string multiply(string num1, string num2) {
        string res="";
        if(num1.empty()) return num2;
        if(num2.empty()) return num1;
        if(num1[0]=='0' || num2[0]=='0') return "0";
        int n = num1.length();
        for(int i=n-1; i>=0; --i)
        {
            string str = multiplyOneDigit(num2, num1[i]-'0');
            res = add(res, str, n-i-1);
        }
        reverse(res.begin(), res.end());
        return res;
    }
};
```

Simulate the process of multiple two numbers:

1. Using one digit of `num2` from right to left, multiply by `num1` to get a template value `str`.
2. Add the `str` (needs to match the position) to the result.

**Complexity:**

* **worst-case time complexity:** `O(n1 * n2)`, where `n1` is the length of `num1`, `n2` is the length of `num2`.
* **worst-case space complexity:** `O(n1 + n2)`, where `n1` is the length of `num1`, `n2` is the length of `num2`.

### Solution 2

* C++
```
string multiply(string num1, string num2) {
    long ns1=num1.size(), ns2=num2.size(); //Why use long?
    if(ns1==0 || ns2==0) return "0";
    int n1, n2, sum, carry;
    vector<int> dp(ns1+ns2, 0);
    for(long i=0; i<ns1; ++i)
    {
        n1 = num1[ns1-i-1] - '0';
        carry=0;
        for(long j=0; j<ns2; ++j)
        {
            n2 = num2[ns2-j-1] - '0';
            sum = n1*n2 + dp[i+j] + carry;
            carry = sum/10;
            dp[i+j] = sum%10;
        }
        if(carry>0) dp[i+ns2] += carry;
    }
    long start=ns1+ns2-1;
    while(start>=0 && dp[start]==0) start--;
    if(start==-1) return "0";
    string res = "";
    for(long i=start; i>=0; --i) res += '0' + dp[i];
    return res;
}
```

Using `dp[i+j]` to store the result from multiply of `num1[ns1-i-1]` and `num2[ns2-j-1]`. 

**Complexity:**

* **worst-case time complexity:** `O(n1 * n2)`, where `n1` is the length of `num1`, `n2` is the length of `num2`.
* **worst-case space complexity:** `O(n1 + n2)`, where `n1` is the length of `num1`, `n2` is the length of `num2`.
