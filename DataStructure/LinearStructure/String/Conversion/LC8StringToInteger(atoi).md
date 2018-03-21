# LC8 String to Integer (atoi)

### LeetCode

## Question

Implement atoi to convert a string to an integer.

**Hint**: Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

**Notes**: It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

**Requirements for atoi:**

The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

If no valid conversion could be performed, a zero value is returned. If the correct value is out of the range of representable values, INT_MAX (2147483647) or INT_MIN (-2147483648) is returned.


## Solutions
* C++1
```
int myAtoi(string str) {
        long res = 0;
        int sign = 1;
        int i = str.find_first_not_of(" ");
        if(str[i]=='-' || str[i]=='+')
        {
            if(str[i] == '-') sign = -1;
            i++;
        }
        while(isdigit(str[i]))
        {
            res = res*10 + str[i++]-'0';
            if(res*sign <= INT_MIN) return INT_MIN;
            if(res*sign >= INT_MAX) return INT_MAX;
        }
        return sign * res;
}
```

* Java1
```
public int myAtoi(String str) {
        if(str.isEmpty()) return 0;
        int res=0, sign=1;
        int base = Integer.MAX_VALUE/10;
        int i=0;
        str = str.trim();
        if(str.charAt(i)=='-' || str.charAt(i)=='+')
            sign = (str.charAt(i++)=='+') ? 1 : -1;
        for(; i<str.length() && Character.isDigit(str.charAt(i)); ++i)
        {
            if(res>base || (res==base && str.charAt(i)>'7'))
                return (sign==1) ? Integer.MAX_VALUE : Integer.MIN_VALUE;
            res = 10*res + (str.charAt(i) - '0');
        }
        return sign * res;
    }
```