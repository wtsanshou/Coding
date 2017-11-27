# LC258. Add Digits

### LeetCode

## Question

Given a non-negative integer num, repeatedly add all its digits until the result has only one digit.

**For example:**

Given num = 38, the process is like: 3 + 8 = 11, 1 + 1 = 2. Since 2 has only one digit, return it.

Follow up: Could you do it without any loop/recursion in O(1) runtime?

**Hint:**

* A naive implementation of the above process is trivial. Could you come up with other methods?
* What are all the possible results?
* How do they occur, periodically or randomly?
* You may find this Wikipedia article useful.

## Solutions

* C++1
```
int addDigits(int num) {
    return (num!=0 && num%9==0) ? 9 : num%9;
}
```

##Explanation

if you list all results from 0 to 30, you may see some rule. the results periodically occur.

```
0~9 (10 nums) :      0,1,2,3,4,5,6,7,8,9
10~18(9 nums):         1,2,3,4,5,6,7,8,9
19~27(9 nums):         1,2,3,4,5,6,7,8,9
and so on
```

only need to be careful about 0 and the multiples of 9.