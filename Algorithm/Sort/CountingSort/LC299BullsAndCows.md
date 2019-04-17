# LC299. Bulls and Cows

### LeetCode

## Question

You are playing the following Bulls and Cows game with your friend: You write down a number and ask your friend to guess what the number is. Each time your friend makes a guess, you provide a hint that indicates how many digits in said guess match your secret number exactly in both digit and position (called "bulls") and how many digits match the secret number but locate in the wrong position (called "cows"). Your friend will use successive guesses and hints to eventually derive the secret number.

**For example: **
```
Secret number:  "1807"
Friend's guess: "7810"
Hint: 1 bull and 3 cows. (The bull is 8, the cows are 0, 1 and 7.)
```

Write a function to return a hint according to the secret number and friend's guess, use A to indicate the bulls and B to indicate the cows. In the above example, your function should return "1A3B".

Please note that both secret number and friend's guess may contain duplicate digits, for example:

```
Secret number:  "1123"
Friend's guess: "0111"
In this case, the 1st 1 in friend's guess is a bull, the 2nd or 3rd 1 is a cow, and your function should return "1A1B".
```

You may assume that the secret number and your friend's guess only contain digits, and their lengths are always equal.

## Solutions

### Solution 1

* C++
```
string getHint(string secret, string guess) {
    int se[10] = {0};
    int gu[10] = {0};
    int bull = 0, cow=0;
    for(int i=0; i<secret.length(); ++i)
    {
        if(secret[i]==guess[i]) bull++;
        else
        {
            se[secret[i]-'0']++;
            gu[guess[i]-'0']++;
        }
    }
    for(int i=0; i<10; ++i)
        cow += min(se[i], gu[i]);
    return to_string(bull)+'A'+to_string(cow)+'B';
}
```

Using two array to count the digital of the `secret` and `guess` respectively as `cow`. `bull` is easy to count.

**Complexity**

* **worst-case time complexity:** `O(N)`, where `N` is the length of `secret` or `guess`
* **worst-case space complexity:** O(1)

### Solution 2 

* C++
```string getHint(string secret, string guess) {
    int bc[10] = {0}, a = 0, b = 0;
    for(int i=0; i<secret.size(); i++)
    {
        if(secret[i] == guess[i])
            a++;
        else
        {
            int si = secret[i] - '0';
            int gi = guess[i] - '0';
            if(bc[si]++<0) b++;
            if(bc[gi]-->0) b++;
        }
    }
    return to_string(a)+"A" + to_string(b) + "B";
}
```

Only one array is needed to count the `cow`. count plus on `secret` and count minus on `guess`. 

**Complexity**

* **worst-case time complexity:** `O(N)`, where `N` is the length of `secret` or `guess`
* **worst-case space complexity:** O(1)
