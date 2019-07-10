# LC9. Palindrome Number

### LeetCode

## Question

Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

**Example 1:**
```
Input: 121
Output: true
```

**Example 2:**

```
Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
```

**Example 3:**
```
Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```

**Follow up:** 

* Do this without extra space.
* Coud you solve it without converting the integer to a string?

## Solutions

### Solution 1

* C++ (222ms)
```
bool isPalindrome(int x) {
    if(x < 0) return false;
    int n = x;
    long res = 0;
    while(n>0)
    {
        res = res*10 + n%10;
        n/=10;
    }
    return res==x;
}
```

* Java
```
public boolean isPalindrome(int x) {
    if(x < 0) return false;
    int n = x;
    long reverse = 0;
    while(n > 0){
        reverse = reverse*10 + (n%10);
        n /= 10;
    }
    return reverse == x;
}
```

Reverse the number is easy. But be careful some corner cases:

1. The reversed number could be exceed integer range.
2. All negative numbers are not palindrome
3. Don't use x directly, the orignal x need to be used in the end.

**Complexity:**

* **worst-case time complexity:** `O(1)`.  
* **worst-case space complexity:** `O(1)`. 
