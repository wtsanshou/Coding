# LC640. Solve the Equation

### LeetCode

## Question

Solve a given equation and return the value of `x` in the form of string `"x=#value"`. The equation contains only '`+`', '`-`' operation, the variable `x` and its coefficient.

If there is no solution for the equation, return `"No solution"`.

If there are infinite solutions for the equation, return `"Infinite solutions"`.

If there is exactly one solution for the equation, we ensure that the value of `x` is an integer.

**Example 1:**
```
Input: "x+5-3+x=6+x-2"
Output: "x=2"
```

**Example 2:**
```
Input: "x=x"
Output: "Infinite solutions"
```

**Example 3:**
```
Input: "2x=x"
Output: "x=0"
```

**Example 4:**
```
Input: "2x+3x-6x=x+2"
Output: "x=-1"
```

**Example 5:**
```
Input: "x=x+2"
Output: "No solution"
```

## Solutions

* Java1
```
class Solution {
    
    private int n_pre_x = 0, xSign = 1;
    private int value = 0, valueSign = -1;
    private String num = "";
    private int sign = 1;
    
    public String solveEquation(String equation) {
        calculateNpreviousXandRightHandSide(equation);
        return result(n_pre_x, value);
    }
    
    private void calculateNpreviousXandRightHandSide(String equation){
        char[] equ = equation.toCharArray();
        for(char c : equ){
            if(c == 'x'){
                addAValueToNpreviousX();
                num = "";
            }
            else if(c == '+'){
                addAValueToRightHandSide();
                setSignAndInitialNum(1);
            }
            else if(c == '-'){
                addAValueToRightHandSide();
                setSignAndInitialNum(-1);
            }
            else if(c == '='){
                addAValueToRightHandSide();
                setSignAndInitialNum(1);
                xSign *= -1;
                valueSign *= -1;
            }
            else{
                num += c;
            }
        }
        addAValueToRightHandSide();
    }
    
    private void addAValueToNpreviousX(){
        n_pre_x += (num.isEmpty() ? 1 : Integer.valueOf(num)) * xSign * sign;
    }
    
    private void addAValueToRightHandSide(){
        value += getStringValue(num, valueSign, sign);
    }
    
    private void setSignAndInitialNum(int sign){
        this.sign = sign;
        num = "";
    }
    
    private int getStringValue(String num, int valueSign, int sign){
        return (num.isEmpty() ? 0 : Integer.valueOf(num)) * valueSign * sign;
    }
    
    private String result(int n, int value){
        if(n==0 && value==0) return "Infinite solutions";
        else if(n==0) return "No solution";
        return "x=" + (value/n);
    }
}
```

## Explanation

The idea is to move all x's coefficients to left and move all integer values to the right hand side. Just be careful the signs between the left and right sides of the `=`.

**Cases:**

1. sum of x's coefficients equals `0` `&&` right hand side equals `0`, then there is "Infinite solutions".
2. sum of x's coefficients equals `0` but right hand side doesn't equal `0`, then there is "No solution".
3. sum of x's coefficients and right hand side both side doesn't equal `0`, then the result is `"x=" + (value/n)`.

**Corner case:** `0x=0`, `0x=1`

* **worst-case time complexity:** O(N), where `N` is the length of the input String `equation`.
* **worst-case space complexity:** O(N), where `N` is the length of the input String `equation`.