# LC394. Decode String

### LeetCode

## Question

Given an encoded string, return it's decoded string.

The encoding rule is: `k[encoded_string]`, where the `encoded_string` inside the square brackets is being repeated exactly `k` times. Note that `k` is guaranteed to be a positive integer.

You may assume that the input string is always valid; No extra white spaces, square brackets are well-formed, etc.

Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, `k`. For example, there won't be input like `3a` or `2[4]`.

**Examples:**
```
s = "3[a]2[bc]", return "aaabcbc".
s = "3[a2[c]]", return "accaccacc".
s = "2[abc]3[cd]ef", return "abcabccdcdcdef".
```

## Solutions

* C++1 (0ms) O(n)
```
string decodeString(string s) {
    int n = 0;
    string word="";
    stack<int> repeat;
    stack<string> words;
    for(auto c : s)
    {
        if(isdigit(c))
            n = 10*n + (c-'0');
        else if(c=='[')
        {
            repeat.push(n);
            n=0;
            words.push(word);
            word.clear();
        }
        else if(c==']')
        {
            int rep = repeat.top();
            repeat.pop();
            while(rep-- > 0)
                words.top() += word;
            word = words.top();
            words.pop();
        }
        else
            word += c;
    }
    return words.empty() ? word : words.top();
}
```

## Explanation

Using two stacks, one for the words that are required to be repeated; one for the cooresponding numbers of repeated times.

* **worst-case time complexity:** O(N), where `N` is the length of input string `s`.
* **worst-case space complexity:** O(N), where `N` is the length of input string `s`.