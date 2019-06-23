# Codility. Longest Password

### Codility

## Question

You would like to set a password for a bank account. However, there are three restrictions on the format of the password:

* it has to contain only alphanumerical characters (a−z, A−Z, 0−9);
* there should be an even number of letters;
* there should be an odd number of digits.

You are given a string S consisting of N characters. String S can be divided into words by splitting it at, and removing, the spaces. The goal is to choose the longest word that is a valid password. You can assume that if there are K spaces in string S then there are exactly K + 1 words.

For example, given "test 5 a0A pass007 ?xy1", there are five words and three of them are valid passwords: "5", "a0A" and "pass007". Thus the longest password is "pass007" and its length is 7. Note that neither "test" nor "?xy1" is a valid password, because "?" is not an alphanumerical character and "test" contains an even number of digits (zero).

**Write a function:**

`int solution(string &S);`

that, given a non-empty string S consisting of N characters, returns the length of the longest word from the string that is a valid password. If there is no such word, your function should return −1.

For example, given S = "test 5 a0A pass007 ?xy1", your function should return 7, as explained above.

**Assume that:**

* N is an integer within the range [1..200];
* string S consists only of printable ASCII characters and spaces.

In your solution, focus on correctness. The performance of your solution will not be the focus of the assessment.

## Solutions

### Solution 1

* C++
```
#include <algorithm>
#include <sstream>
#include <cstring>
#include <vector>
vector<string> getWords(string S)
{
    stringstream ss(S);
    vector<string> res;
    string token;
    while(getline(ss, token, ' '))
        res.push_back(token);
    return res;
}

int check(string word)
{
    int alp=0, digit=0;
    for(char w : word)
    {
        if(isalpha(w)) alp++;
        else if(isdigit(w)) digit++;
        else return 0;
    }
    return (alp%2==0 && digit%2!=0) ? alp+digit : 0;
}

int solution(string &S) {
    // write your code in C++14 (g++ 6.2.0)
    vector<string> words = getWords(S);
    int res = 0;
    for(string word : words)
        res = max(res, check(word));
    return res==0 ? -1 : res;
}
```

* C++
```
int check(string word)
{
    int alp=0, digit=0;
    for(char w : word)
    {
        if(isalpha(w)) alp++;
        else if(isdigit(w)) digit++;
        else return -1;
    }
    return (alp%2==0 && digit%2!=0) ? alp+digit : -1;
}

int solution(string &S) {
    // write your code in C++14 (g++ 6.2.0)
    vector<string> words = getWords(S);
    int res = -1;
    for(string word : words)
        res = max(res, check(word));
    return res;
}
```

Count the number of letters and digits. Check if it's even number of letters and odd number of digits.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `S`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of `S`.

