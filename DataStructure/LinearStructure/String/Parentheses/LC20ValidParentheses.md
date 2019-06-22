# LC20. Valid Parentheses

### LeetCode

## Question

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

* Open brackets must be closed by the same type of brackets.
* Open brackets must be closed in the correct order.

Note that an empty string is also considered valid.

**Example 1:**
```
Input: "()"
Output: true
```

**Example 2:**
```
Input: "()[]{}"
Output: true
```

**Example 3:**
```
Input: "(]"
Output: false
```

**Example 4:**
```
Input: "([)]"
Output: false
```

**Example 5:**
```
Input: "{[]}"
Output: true
```

## Solutions

### Solution 1

* C++ (0ms)
```
bool isValid(string s) {
    stack<char> store;
    for(auto c : s)
    {
        if(c=='(' || c=='[' || c=='{') 
            store.push(c);
        else if(!store.empty() && (c-store.top() == 1 || c-store.top() == 2))
            store.pop();
        else 
            return false;
    }
    return store.empty();
}
```

* Java (1ms)
```
public boolean isValid(String s) {
    char[] ss = s.toCharArray();
    Stack<Character> stack = new Stack<Character>();
    for(char c : ss)
    {
        if(c=='(' || c=='[' || c=='{')
            stack.push(c);
        else if(!stack.empty() && (c-stack.peek() == 1 || c-stack.peek() == 2))
            stack.pop();
        else
            return false;
    }
    return stack.empty();
}
```

* Java (1ms)
```
public boolean isValid(String s) {
    char[] ss = s.toCharArray();
    Stack<Character> stack = new Stack<Character>();
    for(char c : ss)
    {
        if(c=='(' || c=='[' || c=='{')
            stack.push(c);
        else if(!stack.empty())
        {
            char top = stack.pop();
            int valid = c - top;
            if(valid!=1 && valid!=2) 
                return false;
        }
        else
            return false;
    }
    return stack.empty();
}
```

### Codility

* Java
```
public int solution(String S) {
    // write your code in Java SE 8
    if(S.length() % 2 != 0) return 0;
    Deque<Character> stack = new LinkedList<>();
    for(char c : S.toCharArray()){
        if(c==')' || c==']' || c=='}'){
            if(stack.isEmpty()) return 0;
            char open = stack.pop();
            if(c==')' && open!='(' 
            || c==']' && open!='['
            || c=='}' && open!='{')
                return 0;
        }
        else stack.push(c);
    }
    return stack.isEmpty() ? 1 : 0;
}
```

* C++ (9ms) 
```
bool isValid(string s) {
    if(s.length()%2 != 0) return false; //3ms
    int diff1 = ')'-'(';
    int diff2 = ']'-'[';
    int diff3 = '}'-'{';
    stack<char> brackets;
    for(char c : s)
    {
        if(c==')' || c==']' || c=='}')
        {
            if(brackets.empty()) return false;
            char diff = c - brackets.top();
            brackets.pop();
            if(diff!= diff1 && diff!=diff2 && diff!=diff3) return false;
        }
        else
            brackets.push(c);
    }
    return brackets.empty();
}
```

Using stack to store the open brackets. When met a close bracket, pop one from the stack. A valid string will always match the open and close brackets.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `s`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of `s`.





