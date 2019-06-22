# LC415. Add Strings

### LeetCode

## Question

Given two non-negative integers num1 and num2 represented as string, return the sum of num1 and num2.

**Note:**

1.	The length of both num1 and num2 is < 5100.
2.	Both num1 and num2 contains only digits 0-9.
3.	Both num1 and num2 does not contain any leading zero.
4.	You must not use any built-in BigInteger library or convert the inputs to integer directly.

## Solutions

### Solution 1

* C++ (3ms)
```
string addStrings(string num1, string num2) {
    int i=num1.length()-1, j=num2.length()-1, carry = 0;
    if(i < j) return addStrings(num2, num1);
    for(; i>=0 && (j>=0 || carry>0); i--, j--)
    {
        int a = num1[i]-'0';
        int b = (j>=0) ? num2[j]-'0' : 0;
        int sum = a+b+carry;
        carry = sum/10;
        num1[i] = (sum%10) + '0';
    }
    return (carry) ? "1"+num1 : num1;
}
```

* C++ (13ms)
```
string addStrings(string num1, string num2) {
    int i=num1.length()-1, j=num2.length()-1, carry = 0;
    string res = "";
    for(;i>=0 || j>=0 || carry>0; i--, j--)
    {
        int a = (i>=0) ? num1[i]-'0' : 0;
        int b = (j>=0) ? num2[j]-'0' : 0;
        int sum = a+b+carry;
        carry = sum/10;
        res = to_string(sum%10) + res;
    }
    return res;
}
```

* C++ (16ms)
```
string addStrings(string num1, string num2) {
    int i=num1.length()-1, j=num2.length()-1;
    int carry = 0;
    string res = "";
    while(i>=0 || j>=0 || carry>0)
    {
        carry = carry + ((i>=0) ? num1[i--]-'0' : 0);
        carry += (j>=0) ? num2[j--]-'0' : 0;
        res = to_string(carry%10) + res;
        carry /= 10;
    }
    return res;
}
```

Add digits of `num1` and `num2` from right to left. 

**Note** the final `carry`.

**Complexity:**

* **worst-case time complexity:** `O(max(n1, n2))`, where `n1` is the length of `num1`, `n2` is the length of `num2`.
* **worst-case space complexity:** `O(1)`.