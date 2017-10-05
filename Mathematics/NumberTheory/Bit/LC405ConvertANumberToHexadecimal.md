# LC405. Convert a Number to Hexadecimal

### LeetCode

## Question

Given an integer, write an algorithm to convert it to hexadecimal. For negative integer, <a href="https://en.wikipedia.org/wiki/Two%27s_complement">two’s complement</a> method is used.

**Note:**

1. All letters in hexadecimal (a-f) must be in lowercase.
2. The hexadecimal string must not contain extra leading 0s. If the number is zero, it is represented by a single zero character '0'; otherwise, the first character in the hexadecimal string will not be the zero character.
3. The given number is guaranteed to fit within the range of a 32-bit signed integer.
4. You must not use any method provided by the library which converts/formats the number to hex directly.

**Example 1:**

**Input:**
```
26
```

**Output:**
```
"1a"
```

**Example 2:**

**Input:**
```
-1
```

**Output:**
```
"ffffffff"
```

## Solution

* C++1 (0ms)
```
string toHex(int num) {
    if(num==0) return "0";
    string res;
    for(int count=0; num!=0 && count<8; ++count)
    {
        int temp = num & 15;
        if(temp < 10) res += to_string(temp);
        else res +=('a'+(temp-10));
        num = num>>4;
    }
    reverse(res.begin(), res.end());
    return res;
}
```

* C++2 (6ms)
```
string toHex(int num) {
    if(num==0) return "0";
    string res;
    for(int count=0; num!=0 && count<8; ++count)
    {
        int temp = num & 15;
        if(temp < 10) res = to_string(temp) + res;
        else res = res.insert(0, 1, ('a'+(temp-10)));
        num = num>>4;
    }
    return res;
}
```

## Explanation

Check 4 bits each time to get a Hexadecimal

**NOTE** corner cases:
1. num == 0

* **worst-case time complexity:** O(log<sub>16</sub>(n))
* **worst-case space complexity:** O(1).

