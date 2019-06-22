# LC187. Repeated DNA Sequences

### LeetCode

## Question

All DNA is composed of a series of nucleotides abbreviated as A, C, G, and T, for example: "ACGAATTCCG". When studying DNA, it is sometimes useful to identify repeated sequences within the DNA.

Write a function to find all the 10-letter-long sequences (substrings) that occur more than once in a DNA molecule.

**For example**
```
Given s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT",

Return:
["AAAAACCCCC", "CCCCCAAAAA"].
```

## Solutions

### Solution 1

* C++
```
vector<string> findRepeatedDnaSequences(string s) {
    unordered_map<string, int> map;
    vector<string> res;
    int n = s.length()-10;
    for(int i=0; i<=n; ++i) //for(int i=0; i<=s.length()-10; ++i) has error, don’t know why!
    {
        string sub = s.substr(i, 10);
        if(map[sub]==1) res.push_back(sub);
        map[sub]++;
    }
    return res;
}
```

Using a map to count all 10-letter-long substring in `s`. When found a duplicated sequence, put it into result.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `s`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of `s`.