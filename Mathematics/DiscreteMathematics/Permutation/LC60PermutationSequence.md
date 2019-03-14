# LC60. Permutation Sequence

### LeetCode

## Question

The set [1,2,3,…,n] contains a total of n! unique permutations.
By listing and labeling all of the permutations in order,
We get the following sequence (ie, for n = 3):

1.	"123"
2.	"132"
3.	"213"
4.	"231"
5.	"312"
6.	"321"

Given n and k, return the kth permutation sequence.

**Note:** Given n will be between 1 and 9 inclusive.

## Solutions

### Solution 1

* C++1
```
string getPermutation(int n, int k) {
    vector<char> digits(n);
    vector<int>factorials(n+1);
    factorials[0] = 1;
    int fSum = 1;
    for(int i=1; i<=n; ++i)
    {
        digits[i-1] = '0'+i; //digits[n] = {1,2,3,..., n};
        fSum *= i;
        factorials[i] = fSum;  //int fac[9] = {1, 1, 2, 6, 24, 120, 720, 5040, 40320};
    }

    string res;
    k -= 1;
    for(int i=n-1; i>=0; --i)
    {
        int th = k/factorials[i];
        res += digits[th];
        digits.erase(digits.begin()+th);
        k %= factorials[i];
    }

    return res;
}
```

* C++2
```
string getPermutation(int n, int k) {
    vector<char> digit;
    for(int i=1; i<=n; ++i) digit.push_back('0'+i);
    int fac[9] = {1, 1, 2, 6, 24, 120, 720, 5040, 40320};
    string res="";
    k -= 1;
    for(int i=n; i>=1; --i)
    {
        int th = k/fac[i-1];
        res += digit[th];
        digit.erase(digit.begin()+th);
        k %= fac[i-1];
    }
    return res;
}
```

* C++3
```
class Solution {
public:
    char getThEmpty(vector<bool>& digit, int th)
    {
        int cnt =0;
        for(int i=0; i<digit.size(); ++i)
        {
            if(digit[i]==false)
            {
                if(cnt==th)
                {
                    digit[i] = true;
                    return '0'+i+1;
                }
                cnt++;
            }
        }
        return '0';
    }

    string getPermutation(int n, int k) {
        vector<bool> digit(n, false);
        int fac[8] = {1, 2, 6, 24, 120, 720, 5040, 40320};
        string res="";
        for(int i=n-1; i>=1; --i)
        {
            int th = (k-1)/fac[i-1];
            res += getThEmpty(digit, th);
            k %= fac[i-1];
            if(k==0) break;
        }
        for(int i=n-1; i>=0; --i)
        {
            if(digit[i]==false)
            {
                digit[i]==true;
                res += '0'+i+1;
            }
        }
        return res;
    }
};
```

For example n = 4, you have {1, 2, 3, 4}

All the permutations you have:

```
1 + permutations(2, 3, 4)
2 + permutations(1, 3, 4)
3 + permutations(1, 2, 4)
4 + permutations(1, 2, 3)
```

The number of permutations of n numbers equals `n!`. So each of those with permutations of 3 numbers means there are 6 (`factorials[3]`) possible permutations. Meaning there would be a total of 24 (`factorials[4]`) permutations in this particular one. 

Suppose we are looking for the (k = 14) `14th permutation`.

Because the first 2 subset has 12 permutations, the 14th permutation must be in the:

`3 + permutations(1, 2, 4)` subset.

Next, we need to find the 2th permutation in the `permutations(1, 2, 4)`. The same as above:

```
1 + permutations(2, 4)
2 + permutations(1, 4)
4 + permutations(1, 2)
```

The 2th permutation in the `permutations(1, 2, 4)` must be in the:

`1 + permutations(2, 4)` subset.

Next, we need to find the 2th permutation in the `permutations(2, 4)`. The same as above:

```
2 + permutations(4)
4 + permutations(2)
```

The 2th permutation in the `permutations(2, 4)` must be in the:

`4 + permutations(2)` subset

Next, we need to find the 1th permutation in the `permutations(2)` which is `2` itself.

Finally, we get the 14th permutation `(3, 1, 4, 2)`.

* **worst-case time complexity:** `O(1)`. 
* **worst-case space complexity:** `O(1)`

