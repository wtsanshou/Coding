# LC9. Palindrome Number

### LeetCode

## Question

Determine whether an integer is a palindrome. Do this without extra space.

## Solutiona

### Solution 1

* C++ (222ms)
```
bool isPalindrome(int x) {
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

One way to verify palindrome is to get a version of a reversed input, then compare the reversed and the original inputs. This way is very suitable for this question.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `x`.  
* **worst-case space complexity:** `O(1)`.