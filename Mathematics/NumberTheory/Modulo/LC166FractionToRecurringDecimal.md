# LC166. Fraction to Recurring Decimal

### LeetCode

## Question

Given two integers representing the numerator and denominator of a fraction, return the fraction in string format.

If the fractional part is repeating, enclose the repeating part in parentheses.

**For example**
```
•	Given numerator = 1, denominator = 2, return "0.5".
•	Given numerator = 2, denominator = 1, return "2".
•	Given numerator = 2, denominator = 3, return "0.(6)".
```

## Solutions

### Solution 1
* C++
```
string fractionToDecimal(int numerator, int denominator) {
    if(numerator==0) return "0";
    long n = numerator, d = denominator;
    string res;
    if(n<0 ^ d<0) res += "-";
    n = abs(n);
    d = abs(d);
    res += to_string(n/d);
    if(n%d == 0) return res;
    res += ".";
    unordered_map<int, int> map;
    for(long i=n%d; i!=0; i%=d)
    {
        if(map.count(i) > 0)
        {
            res.insert(map[i],1, '(');
            res += ")";
            break;
        }
        map[i] = res.size();
        i *= 10;
        res += to_string(i/d);
    }
    return res;
}
```

**Note:**

1. sign
2. Ask what happened if `denominator` is `0`
3. If the mod `i` repeat, the fractional part will be repeated.
4. `numerator` might be very big, is miltiply by 10, it may be larger than maximum integer.