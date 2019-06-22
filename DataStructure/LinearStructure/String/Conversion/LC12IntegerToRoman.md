# LC13.	Integer to Roman

### LeetCode

## Question

Given an integer, convert it to a roman numeral.

Input is guaranteed to be within the range from 1 to 3999.

## Solutions

### Solution 1

* C++
```
string intToRoman(int num) {
    string M[] = {"", "M", "MM", "MMM"};
    string C[] = {"", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"};
    string X[] = {"", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"};
    string I[] = {"", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"};
    return M[num/1000] + C[(num%1000)/100] + X[(num%100)/10] + I[num%10];
}
```

* Java
```
public class Solution { 
    private String THOUSAND[] = {"", "M", "MM", "MMM"};
    private String HUNDURD[] = {"", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM"};
    private String TEN[] = {"", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC"};
    private String DIGIT[] = {"", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX"};
    
    public String intToRoman(int num) {
        return THOUSAND[num/1000] + HUNDURD[(num%1000)/100] + TEN[(num%100)/10] + DIGIT[num%10];
    }
}
```

The main idea is to cout the number of THOUSAND, HUNDURD, TEN, and DIGIT.

Different number map to different String.



