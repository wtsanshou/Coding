# LC13. Roman to Integer

### LeetCode

## Question

Given a roman numeral, convert it to an integer.

Input is guaranteed to be within the range from 1 to 3999.

## Solutions

### Solution 1

* C++ (44ms)
```
int romanToInt(string s) {
    int sum = 0;
    char pre = 0;
    int i, len=s.length();
    for(i=0; i<len; i++)
    {
        switch(s[i])
        {
            case 'I':
                sum+=1; pre = 'I'; break;
            case 'V':
                sum+=5;
                if(pre == 'I') sum-=2;
                pre = 'V'; break;
            case 'X':
                sum+=10;
                if(pre == 'I') sum-=2;
                pre = 'X'; break;
            case 'L':
                sum+=50;
                if(pre == 'X') sum-=20;
                pre = 'L'; break;
            case 'C':
                sum+=100;
                if(pre == 'X') sum-=20;
                pre = 'C'; break;
            case 'D':
                sum+=500;
                if(pre == 'C') sum-=200;
                pre = 'D'; break;
            case 'M':
                sum+=1000;
                if(pre == 'C') sum-=200;
                pre = 'M'; break;
        }
    }
    return sum;
}
```

```
THOUSAND[] = {"", "M", "MM", "MMM"};
HUNDURD[] = {"", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"};
TEN[] = {"", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"};
DIGIT[] = {"", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"};
```

, "IX", "XL", "XC", "CD", and "CM" are the previous number of next level roman letter. They can be represented as separted single roman letters.

**For example:**

```
"IV" = "V" - "I" = "I" + "V" - 2*"I"
```

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `s`.
* **worst-case space complexity:** `O(1)`.