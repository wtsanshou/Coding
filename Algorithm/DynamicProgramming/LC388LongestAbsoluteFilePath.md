# LC388. Longest Absolute File Path

### LeetCode

## Question

Suppose we abstract our file system by a string in the following manner:
The string "`dir\n\tsubdir1\n\tsubdir2\n\t\tfile.ext`" represents:

```
dir
    subdir1
    subdir2
        file.ext
```

The directory dir contains an empty sub-directory subdir1 and a sub-directory subdir2 containing a file `file.ext`.

The string "`dir\n\tsubdir1\n\t\tfile1.ext\n\t\tsubsubdir1\n\tsubdir2\n\t\tsubsubdir2\n\t\t\tfile2.ext`" represents:

```
dir
    subdir1
        file1.ext
        subsubdir1
    subdir2
        subsubdir2
            file2.ext
```

The directory dir contains two sub-directories subdir1 and subdir2. subdir1 contains a file `file1.ext` and an empty second-level sub-directory subsubdir1. subdir2contains a second-level sub-directory subsubdir2 containing a file `file2.ext`.

We are interested in finding the longest (number of characters) absolute path to a file within our file system. For example, in the second example above, the longest absolute path is "`dir/subdir2/subsubdir2/file2.ext`", and its length is 32 (not including the double quotes).

Given a string representing the file system in the above format, return the length of the longest absolute path to file in the abstracted file system. If there is no file in the system, return 0.

**Note:**

•	The name of a file contains at least a . and an extension.
•	The name of a directory or sub-directory will not contain a `.`.

Time complexity required: O(n) where n is the size of the input string.

Notice that `a/aa/aaa/file1.txt` is not the longest file path, if there is another path `aaaaaaaaaaaaaaaaaaaaa/sth.png`.

## Solutions

### Solution 1

* C++
```
int lengthLongestPath(string input) {
    vector<int>dp(1,0);
    int res = 0;
    stringstream ss(input);
    string block;
    while(getline(ss, block, '\n'))
    {
        int i = block.find_first_not_of('\t')+1;
        if(i>=dp.size())
            dp.push_back(0);
        dp[i] = dp[i-1]+block.size()-i+2; //include "/"
        if(block.find('.') != string::npos)
            res = max(res, dp[i]-1);
    }
    return res;
}
```

* C++
```
int lengthLongestPath(string input) {
    vector<int> dp;
    int longest = 0;
    stringstream ss(input);
    string cur;
    while(getline(ss, cur, '\n')){
        int i= cur.find_first_not_of('\t');
        if(i+1 > dp.size())
            dp.push_back(0);
        dp[i] = (i-1>=0 ? dp[i-1] : 0) + cur.size()-i+1;
        if(cur.find('.') != string::npos)
            longest = max(longest, dp[i]-1);
    }
    return longest;
}
```

Using `dp[i]` to store the path length of the current layer. Notice file or directory only has one parent `dp[i-1]`.

Only need to check the maximum length when found a file (`cur.find('.')`).

```
dir
    subdir1
        file1.ext
        subsubdir1
    subdir2
        subsubdir2
            file2.ext
```

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the String `input`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the String `input`.