# LC423. Reconstruct Original Digits from English

### LeetCode

## Question

Given a non-empty string containing an out-of-order English representation of digits 0-9, output the digits in ascending order.

**Note:**

1.	Input contains only lowercase English letters.
2.	Input is guaranteed to be valid and can be transformed to its original digits. That means invalid inputs such as "abc" or "zerone" are not permitted.
3.	Input length is less than 50,000.

**Example 1:**

```
Input: "owoztneoer"

Output: "012"
```

**Example 2:**

```
Input: "fviefuro"

Output: "45"
```

## Solutions

### Solution 1

* C++
```
string originalDigits(string s) {
    int letter[128] = {0};
    for(char c : s) letter[c]++;
    int digits[10];
    digits[0] = letter['z'];                                        //only zero has '`g`'
    digits[2] = letter['w'];                                        //only two has 'w'
    digits[4] = letter['u'];                                        //only four has 'u'
    digits[6] = letter['x'];                                        //only six has 'x'
    digits[8] = letter['g'];                                        //only eight has 'g'
    digits[5] = letter['f'] - digits[4];                            //five and four share 'f'
    digits[7] = letter['v'] - digits[5];                            //seven and five share 'v'
    digits[3] = letter['t'] - digits[2] - digits[8];                //three and two, eight share 't'
    digits[1] = letter['o'] - digits[0] - digits[2] - digits[4];    //one and zero, two, four share 'o'
    digits[9] = letter['i'] - digits[5] - digits[6] - digits[8];    //nine and five, six, eight share 'i'
    string res;
    for(int i=0; i<10; ++i)
        if(digits[i] > 0)
            res += string(digits[i], '0'+i);
        // for(int j=0; j<digit[i]; ++j)
        //    res += '0'+i;
    return res;
}
```

Count the number of each letter in `s`.

The numbber digits with unique letter (zero, two, four, six, eight) will not changed. For other digits (five, seven, three, one, and nine), use their count number minus the numbber of unchanged digits who has shared letters.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `s`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of `s`.

