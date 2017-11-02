# LC592. Fraction Addition and Subtraction

### LeetCode

## Question

Given a string representing an expression of fraction addition and subtraction, you need to return the calculation result in string format. The final result should be irreducible fraction. If your final result is an integer, say 2, you need to change it to the format of fraction that has denominator 1. So in this case, 2 should be converted to 2/1.

**Example 1:**

```
Input:"-1/2+1/2"
Output: "0/1"
```

**Example 2:**

```
Input:"-1/2+1/2+1/3"
Output: "1/3"
```

**Example 3:**

```
Input:"1/3-1/2"
Output: "-1/6"
```

**Example 4:**

```
Input:"5/3+1/3"
Output: "2/1"
```

**Note:**

* The input string only contains '0' to '9', '/', '+' and '-'. So does the output.
* Each fraction (input and output) has format ±numerator/denominator. If the first input fraction or the output is positive, then '+' will be omitted.
* The input only contains valid irreducible fractions, where the numerator and denominator of each fraction will always be in the range [1,10]. If the denominator is 1, it means this fraction is actually an integer in a fraction format defined above.
* The number of given fractions will be in the range [1,10].
* The numerator and denominator of the final result are guaranteed to be valid and in the range of 32-bit int.

## Solutions

* C++1
```
class Solution {
public:
    int GCD(int a, int b)
    {
        return b==0 ? a : GCD(b, a%b);
    }
    int LCD(int a, int b)
    {
        int gcd = GCD(a, b);
        return a/gcd * b;
    }
    void add(int (&pre)[2], int cur[2])
    {
        int lcd = LCD(pre[1], cur[1]);
        pre[0] = lcd/pre[1] * pre[0] + lcd/cur[1] * cur[0];
        pre[1] = lcd;
        int gcd = GCD(abs(pre[0]), pre[1]);
        pre[0] /= gcd;
        pre[1] /= gcd;
    }
    string fractionAddition(string expression) {
        if(expression.empty() || expression=="+" || expression=="-") return "0/1";
        int sign = expression[0]=='-' ? -1 : 1;
        int num=0, n = expression.length();
        int pre[2] = {0,1}, cur[2] = {0,1};
        //vector<int> pre(vals, vals+2), cur(vals, vals+2);
        expression += "+";
        for(int i= (expression[0]=='-' ? 1 : 0); i<=n; ++i)
        {
            if(isdigit(expression[i]))
                num = 10*num + (expression[i]-'0');
            else if(expression[i] == '/')
            {
                cur[0] = sign*num;
                num = 0;
            }
            else
            {
                cur[1] = num;
                num=0;
                sign = expression[i]=='-' ? -1 : 1;
                add(pre, cur);
            }
        }
        return to_string(pre[0]) + "/" + to_string(pre[1]);
    }
};
```

## Explanation

Follow the rule of fraction addition. 

1. Calculate the Least Common Denominator `lcd` of the two fractions' denomiators.
2. Add numerator by `lcd/pre[1] * pre[0] + lcd/cur[1] * cur[0]`.
3. Use GCD to remove common divisor of the result fraction.

It might be better to use a `Fraction struct` to replace `pre` and `cur` arrays.
