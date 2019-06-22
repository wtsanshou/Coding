# LC535. Encode and Decode TinyURL

### LeetCode

## Question

**Note:** This is a companion problem to the System Design problem: Design TinyURL.

TinyURL is a URL shortening service where you enter a URL such as `https://leetcode.com/problems/design-tinyurl` and it returns a short URL such as `http://tinyurl.com/4e9iAk`.

Design the encode and decode methods for the TinyURL service. There is no restriction on how your encode/decode algorithm should work. You just need to ensure that a URL can be encoded to a tiny URL and the tiny URL can be decoded to the original URL.

## Solutions

### Solution 1

* C++ (3ms)
```
class Solution {
public:
    vector<string> res;
    // Encodes a URL to a shortened URL.
    string encode(string longUrl) {
        res.push_back(longUrl);
        return to_string(res.size()-1);
    }

    // Decodes a shortened URL to its original URL.
    string decode(string shortUrl) {
        return res[stoi(shortUrl)];
    }
};
```

Here the `shortened URL` is the index of the `original URL` in the array `res`.

* **worst-case time complexity:** `O(1)`.
