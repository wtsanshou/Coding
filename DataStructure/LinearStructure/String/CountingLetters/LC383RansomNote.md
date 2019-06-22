# LC383. Ransom Note

### LeetCode

## Question

Given an arbitrary ransom note string and another string containing letters from all the magazines, write a function that will return true if the ransom note can be constructed from the magazines ; otherwise, it will return false.
Each letter in the magazine string can only be used once in your ransom note.

**Note:**

You may assume that both strings contain only lowercase letters.

```
canConstruct("a", "b") -> false
canConstruct("aa", "ab") -> false
canConstruct("aa", "aab") -> true
```

## Solutions

### Solution 1

* C++ (32ms)
```
bool canConstruct(string ransomNote, string magazine) {
    vector<int> magazLetters(128, 0);
    for(char m : magazine)
        magazLetters[m]++;
    for(char r : ransomNote)
        if(--magazLetters[r]<0) return false;
    return true;
}
```

1. Count the number of each letter in `magazine` and store it in `magazLetters`.
2. Minus number from the `magazLetters` based on the letters in `ransomNote`.
3. If found the number of a letter in `ransomNote` is more than the number of the letter in `magazine`, return false.

**Complexity:**

* **worst-case time complexity:** `O(max(m, n))`, where `m` is the length of `ransomNote`, `n` is the length of `magazine`.
* **worst-case space complexity:** `O(1)`.
