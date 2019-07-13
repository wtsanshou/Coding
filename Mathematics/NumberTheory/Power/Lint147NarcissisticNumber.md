# Lint147. Narcissistic Number

### LintCode

## Questions

Narcissistic Number is a number that is the sum of its own digits each raised to the power of the number of digits. See wiki

For example the 3-digit decimal number 153 is a narcissistic number because 153 = 13 + 53 + 33.

And the 4-digit decimal number 1634 is a narcissistic number because 1634 = 14 + 64 + 34 + 44.

Given n, return all narcissistic numbers with n digits.
You may assume n is smaller than 8.

**Example 1:**
```
Input: 1
Output: [0,1,2,3,4,5,6,7,8,9]
```

**Example 2:**
```
Input:  2
Output: []
Explanation: There is no Narcissistic Number with 2 digits.
```

## Solutions

### Solution 1

* Java
```
public class Solution {
    /**
     * @param n: The number of digits
     * @return: All narcissistic numbers with n digits
     */
    public List<Integer> getNarcissisticNumbers(int n) {
        List<Integer> res = new ArrayList<>();
        if(n==1) res.add(0);
        int start = getEn(n);
        int end = getEn(n+1)-1;
        
        for(int i=start; i<=end; i++){
            if(i == narcissistic(i, n))
                res.add(i);
        }
        
        return res;
    }
    
    private int getEn(int n){
        int res = 1;
        for(int i=1; i<n; i++)
            res *= 10;
        return res;
    }
    
    private int narcissistic(int n, int pow){
        int res = 0;
        while(n>0){
            int digit = n%10;
            res += Math.pow(digit, pow);
            n /= 10;
        }
        return res;
    }
    
}
```

Just used `Brute Force` to check if a number is a Narcissistic number in the range `start` to `end`.

I knew there is a trick way: just directly store the results `[[0,1,2,3,4,5,6,7,8,9],[],[153,370,371,407],[1634,8208,9474],[54748, 92727, 93084],[548834]]` in a list in advance.

I am not sure if there is a mathematics solution.

**Corner Cases:** `0` is one result of `1 digit`

**Complexity:**

* **worst-case time complexity:** O(10<sup>n</sup>), where `n` is the length of the `input`.
* **worst-case space complexity:** O(1).
