# LC22. Generate Parentheses

### LeetCode

## Question

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

**For example**
```
given n = 3, a solution set is:
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

## Solutions

### Solution 1

* C++ (3ms)
```
public:
    void GetParenthesis(vector<string>& res, string aForm, int open, int close)
    {
        if(open==0 && close==0) res.push_back(aForm);
        else if(close>0)
        {
            if(open>0)
            {
                aForm.push_back('(');
                GetParenthesis(res, aForm, open-1, close);
                aForm.pop_back();
            }
            if(close > open)
            {
                aForm.push_back(')');
                GetParenthesis(res, aForm, open, close-1);
                aForm.pop_back();
            }
        }
    }
    vector<string> generateParenthesis(int n) {
        vector<string> res;
        string aForm;
        GetParenthesis(res, aForm, n, n);
        return res;
    }
};
```

`Back tracking` is a normal way to solve this kind of seeking generate all combinations.

Here, only when `open==0 && close==0`, a well-formed parentheses is generated.

There are two chances to `Back tracking` in each recursion:

1. `open>0`
2. `close > open`

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>).  
* **worst-case space complexity:** O(n<sup>2</sup>). 

### Solution 2

* C++ (0ms)
```
class Solution {
public:
    vector<string> res;
    void Helper(string str, int left, int right)
    {
        if(left>0) Helper(str+"(", left-1, right);
        if(right>left) Helper(str+")", left, right-1);
        if(right==0) res.push_back(str);
    }

    vector<string> generateParenthesis(int n) {
        Helper("", n, n);
        return res;
    }
};
```

* Java (2ms)
```
public class Solution {
    
    private List<String> res;
    
    public List<String> generateParenthesis(int n) {
        res = new ArrayList<String>();
        GPhelper("", n, n);
        return res;
    }
    
    private void GPhelper(String arow, int left, int right)
    {
        if(left > 0) GPhelper(arow+"(", left-1, right); //arow will not be changed
        if(right > left) GPhelper(arow+")", left, right-1); // arow is not changed
        if(right == 0) res.add(arow);
    }
}
```

The iteration implementation of the `Back tracking`.

**Complexity:**

* **worst-case time complexity:** O(n<sup>2</sup>).  
* **worst-case space complexity:** O(n<sup>2</sup>). 