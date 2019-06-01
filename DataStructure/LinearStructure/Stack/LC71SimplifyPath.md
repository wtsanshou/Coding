# LC71. Simplify Path

### LeetCode

## Question

Given an absolute path for a file (Unix-style), simplify it.

**For example**
```
path = "/home/", => "/home"
path = "/a/./b/../../c/", => "/c"
```

**Corner Cases:**
```
•	Did you consider the case where path = "/../"?
In this case, you should return "/".
•	Another corner case is the path might contain multiple slashes '/' together, such as "/home//foo/".
In this case, you should ignore redundant slashes and return "/home/foo".
```

## Solutions

### Solution 1

* C++
```
string simplifyPath(string path) {
    string res, token;
    vector<string> temp;
    stringstream ss(path);
    while(getline(ss, token, '/'))
    {
        if(token=="." || token=="") continue;
        else if(token=="..")
        {
            if(!temp.empty()) temp.pop_back();
        }
        else temp.push_back(token);
    }
    for(string str : temp)
        res += "/" + str;
    return res.empty() ? "/" : res;
}
```

Split the `path` by "/". 

Ignore "." and empty string. 

If ".." pop one from the stack, otherwise push in one `token`.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `path`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input `path`.
