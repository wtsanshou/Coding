# LC66. Plus One

### LeetCode

## Question

Given a non-negative integer represented as a non-empty array of digits, plus one to the integer.

You may assume the integer do not contain any leading zero, except the number 0 itself.

The digits are stored such that the most significant digit is at the head of the list.

## Solutions

* C++1 (3ms)
```
vector<int> plusOne(vector<int>& digits) {
    for(int i=digits.size()-1; i>=0;--i)
    {
        if(digits[i] != 9)
        {
            digits[i]++;
            return digits;
        }
        else digits[i]=0;
    }
    digits.insert(digits.begin(), 1);
    return digits;
}
```

* C++2 (4ms)
```
vector<int> plusOne(vector<int>& digits) {
    int i = digits.size();
    if(!i)
    {
        digits.push_back(1);
        return digits;
    }
    int res = digits[i-1] +1;
    int carry = res/10;
    digits[--i] = res%10;
    while(carry && i>0)
    {
        res = digits[--i] +carry;
        carry = res/10;
        digits[i] = res%10;
    }
    if(carry)
        digits.insert(digits.begin(),carry);
    return digits;
}
```

* Java1 (0ms)
```
public int[] plusOne(int[] digits) {
    int n=digits.length;
    for(int i=n-1; i>=0; --i)
    {
        if(digits[i]<9)
        {
            digits[i]++;
            return digits;
        }
        digits[i]=0;
    }
    int[] newDigits = new int[n+1];
    newDigits[0]=1;
    return newDigits;
}
```

## Explanation

Add 1 to each digit from right to left to the digit is less than `9`.

Corner case: all digits are `9`.

* **worst-case time complexity:** O(n)
* **worst-case space complexity:** O(1)