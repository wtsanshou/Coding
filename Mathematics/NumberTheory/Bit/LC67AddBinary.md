# LC67. Add Binary

### LeetCode

## Question

Given two binary strings, return their sum (also a binary string).

**For example**

```
a = "11"
b = "1"
Return "100".
```

## Solutions

### Solution 1

* C++ (8ms)
```
string addBinary(string a, string b) {
    string res ="";
    int re=0, carry=0, i=a.size()-1, j=b.size()-1;

    while(i>=0 && j>=0)
    {
        re = (int)a[i--] + b[j--] + carry - 96;
        carry = re/2;
        res = to_string(re%2) + res;
    }

    while(i>=0)
    {
        re = (int)a[i--] + carry - '0';
        carry = re/2;
        res = to_string(re%2) + res;
    }

    while(j>=0)
    {
        re = (int)b[j--] + carry - '0';
        carry = re/2;
        res = to_string(re%2) + res;
    }

    i=0;
    if(carry) 
        res = to_string(carry) + res;
    else
        while(res[i] == '0') i++;
 
    if(res.substr(i, res.size()-i) == "") return "0";
    return res.substr(i, res.size()-i);
}
```

**Corner cases**

* carry maybe `1` after the three loop.
* Leading `0`.
* The result could be `0`.

**Complexity:**

* **worst-case time complexity:** `O(max(n1, n2))`, where `n1` is the length of the input `a`, `n2` is the length of the input `a`. 
* **worst-case space complexity:** `O(1)`.

### Solution 2

* C++ (6ms)
```
string addBinary(string a, string b) {
    string res="";
    int carry=0, i=a.length()-1, j=b.length()-1;
    while(i>=0 || j>=0 || carry>0)
    {
        int x = (i>=0) ? (a[i--]-'0') : 0;
        int y = (j>=0) ? (b[j--]-'0') : 0;
        int sum = x+y+carry;
        carry = sum/2;
        res = to_string(sum%2) + res;
    }
    res.erase(0, res.find_first_not_of('0'));
    return (res=="") ? "0" : res;
}
```

* C++ (4ms)
```
string addBinary(string a, string b) {
    string res ="";
    int carry=0, i=a.size()-1, j=b.size()-1;
    while(i>=0 || j>=0 || carry==1)
    {
        carry += i>=0 ? (a[i--] - '0') : 0;
        carry += j>=0 ? (b[j--] - '0') : 0;
        res = char(carry%2 + '0') + res;
        carry /= 2;
    }
    i = 0;
    while(res[i] == '0') i++;
    if(res.substr(i, res.size()-i) == "") return "0";
    return res.substr(i, res.size()-i);
}
```

* Java (15ms)
```
public String addBinary(String a, String b) {
    StringBuilder sb = new StringBuilder();
    int i=a.length()-1, j=b.length()-1;
    int carry = 0;
    while(i>=0 || j>=0 || carry>0)
    {
        int av = (i>=0) ? a.charAt(i--)-'0' : 0;
        int bv = (j>=0) ? b.charAt(j--)-'0' : 0;
        int sum = av + bv + carry;
        carry = sum/2;
        sb.insert(0, sum%2);
    }
    return (sb.length()==0) ? "0" : sb.toString().replaceFirst("^0+(?!$)","");
}
```

* Java (5ms)
```
public String addBinary(String a, String b) {
    StringBuilder sb = new StringBuilder();
    int i=a.length()-1, j=b.length()-1;
    int carry = 0;
    while(i>=0 || j>=0 || carry>0)
    {
        int av = (i>=0) ? a.charAt(i--)-'0' : 0;
        int bv = (j>=0) ? b.charAt(j--)-'0' : 0;
        int sum = av + bv + carry;
        carry = sum/2;
        sb.append(sum%2);
    }
    return (sb.length()==0) ? "0" : sb.reverse().toString();
}
```

All in one loop.

**Complexity:**

* **worst-case time complexity:** `O(max(n1, n2))`, where `n1` is the length of the input `a`, `n2` is the length of the input `a`. 
* **worst-case space complexity:** `O(1)`.
