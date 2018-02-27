# LC788. Rotated Digits

### LeetCode

## Question

X is a good number if after rotating each digit individually by 180 degrees, we get a valid number that is different from X. A number is valid if each digit remains a digit after rotation. 0, 1, and 8 rotate to themselves; 2 and 5 rotate to each other; 6 and 9 rotate to each other, and the rest of the numbers do not rotate to any other number.

Now given a positive number N, how many numbers X from 1 to N are good?

**Example:**
```
Input: 10
Output: 4
```

**Explanation:** 

There are four good numbers in the range `[1, 10]` : `2, 5, 6, 9`.

Note that `1` and `10` are not good numbers, since they remain unchanged after rotating.

**Note:**

* `N`  will be in range `[1, 10000]`.

## Solutions

* Java1
```
class Solution {
    public int rotatedDigits(int N) {
        int result = 0;
        for(int i=2; i<=N; ++i){
            if(isRotatedDigit(i))
                result++;
        }
        return result;
    }
    
    private boolean isRotatedDigit(int number){
        boolean all018 = true, has2569 = false;
        while(number != 0){
            int digit = number % 10;
            number /= 10;
            if(is2569(digit))
                has2569 = true;
            else if(isNot018(digit)){
                all018 = false;
                break;
            }
        }
        return all018 && has2569;
    }
    
    private boolean is2569(int digit){
        return digit == 2 || digit == 5 || digit == 6 || digit == 9;
    }
    
    private boolean isNot018(int digit){
        return digit != 0 && digit != 1 && digit != 8;
    }
}
```

## Explanation

The rotated number must:

1. Has at least one digit of `2`, `5`, `6`, or `9`.
2. Any digit in the number must not be `3`, `4`, or `7`.

* **worst-case time complexity:** O(N * D), where `D` is the number of digits in `N`.
* **worst-case space complexity:** O(1)