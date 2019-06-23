# LC451. Sort Characters By Frequency

### LeetCode

## Question

Given a string, sort it in decreasing order based on the frequency of characters.

**Example 1:**

```
Input:
"tree"

Output:
"eert"

Explanation:
'e' appears twice while 'r' and 't' both appear once.
So 'e' must appear before both 'r' and 't'. Therefore "eetr" is also a valid answer.
```

**Example 2:**

```
Input:
"cccaaa"

Output:
"cccaaa"

Explanation:
Both 'c' and 'a' appear three times, so "aaaccc" is also a valid answer.
Note that "cacaca" is incorrect, as the same characters must be together.
```

**Example 3:**

```
Input:
"Aabb"

Output:
"bbAa"

Explanation:
"bbaA" is also a valid answer, but "Aabb" is incorrect.
Note that 'A' and 'a' are treated as two different characters.
```

## Solutions

### Solution 1

* Java (Time Limit Exceeded)
```
public String frequencySort(String s) {
    String[] freq = new String[128];
    for(int i=0; i<freq.length; i++)
        freq[i] = new String();
    
    for(char c : s.toCharArray())
        freq[c] += c;
    Arrays.sort(freq, (a, b) -> b.length()-a.length());
    
    String res = "";
    for(String sub : freq)
        res+=sub;
    return res;
}
```

I was trying to build substring for each character in the String array `freq`. Then sort the array by the length of the substrings in decreasing order.

It seems building the substrings (`freq[c] += c;`) consume too much time.

* Java (41 ms)
```
public String frequencySort(String s) {
    StringBuilder[] freq = new StringBuilder[128];
    for(int i=0; i<freq.length; i++)
        freq[i] = new StringBuilder();
    
    for(char c : s.toCharArray())
        freq[c].append(c);
    Arrays.sort(freq, (a, b) -> b.length()-a.length());
    
    String res = "";
    for(StringBuilder sub : freq)
        res+=sub.toString();
    return res;
}
```

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `s`.
* **worst-case space complexity:** `O(1)`.

### Solution 2

* Java (34 ms)
```
class Solution {
    public String frequencySort(String s) {
        int[] count = new int[128];
        for(char c : s.toCharArray())
            count[c]++;
        
        List<Sub> subs = new ArrayList<>();
        for(int i=0; i<count.length; i++){
            if(count[i]>0)
                subs.add(new Sub((char)i, count[i]));
        }
        
        Collections.sort(subs, (a, b) -> b.freq-a.freq);
        
        StringBuilder res = new StringBuilder();
        for(Sub sub : subs){
            for(int i=0; i<sub.freq; i++)
                res.append(sub.val);
        }
            
        return res.toString();
    }
    
    class Sub{
        char val;
        int freq;
        public Sub(char val, int freq){
            this.val = val;
            this.freq = freq;
        }
    }
}
```

Create a class to represent the frequency of a character. 

Count the number of each character in `s`, then we just consider the character with positive frequency. 

So that we just need to sort the appeared characters.

Finally, use `StringBuilder` to build the final result.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `s`.
* **worst-case space complexity:** `O(1)`.

### Solution 3

* C++ (12ms)
```
class Solution {
public:
    static bool myComp(pair<char,int> a, pair<char,int> b)
    {
        return a.second > b.second;
    }
    string frequencySort(string s) {
        vector<pair<char,int>> freq(256, pair<char,int>());
        for(char c : s)
        {
            freq[c].first = c;
            freq[c].second++;
        }
        sort(freq.begin(), freq.end(), myComp);
        string res;
        for(pair<char, int> pa : freq)
            res += string(pa.second, pa.first);
        return res;
    }
};
```

Using `pair` in `c++` to represent the frequency of a character. 

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `s`.
* **worst-case space complexity:** `O(1)`.