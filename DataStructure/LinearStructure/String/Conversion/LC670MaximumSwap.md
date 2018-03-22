# LC670. Maximum Swap

### LeetCode

## Question

Given a non-negative integer, you could swap two digits **at most** once to get the maximum valued number. Return the maximum valued number you could get.

**Example 1:**
```
Input: 2736
Output: 7236
Explanation: Swap the number 2 and the number 7.
```

**Example 2:**
```
Input: 9973
Output: 9973
Explanation: No swap.
```

**Note:**

* The given number is in the range [0, 10<sup>8</sup>]

## Solutions

* Java1
```
class Solution {
    public int maximumSwap(int num) {
        char[] digits = (String.valueOf(num)).toCharArray();
        for(int i=0; i<digits.length-1; ++i){
            int idOfNextMaxValue = getIdOfNextMaxValue(digits, i+1);
            if(digits[idOfNextMaxValue] > digits[i]){
                mySwap(digits, i, idOfNextMaxValue);
                break;
            }
        }
        return Integer.valueOf(new String(digits));
    }
    
    private int getIdOfNextMaxValue(char[] digits, int next){
        int result = next;
        char max = digits[next];
        for(int i=next+1; i<digits.length; ++i){
            if(digits[i] >= max){
                max = digits[i];
                result = i;
            }
        }
        return result;
    }
    
    private void mySwap(char[] digits, int i, int j){
        char temp = digits[i];
        digits[i] = digits[j];
        digits[j] = temp;
    }
}
```

## Explanation

The left digit is larger, the value of the number is larger.

Traverse from left side of the number, if found the largest digit in the right side which is larger than the current digit, swap them.

**NOTE:** 

1. `swap two digits at most once`
2. Should swap the most right side largest digit.

* **worst-case time complexity:** **O(N<sup>2</sup>)**, where `N` is the length of the number.
* **worst-case space complexity:** **O(N)**, where `N` is the length of the number.