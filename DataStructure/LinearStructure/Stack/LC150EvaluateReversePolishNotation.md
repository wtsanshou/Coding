# LC150. Evaluate Reverse Polish Notation

### LeetCode

## Question

Evaluate the value of an arithmetic expression in Reverse Polish Notation.
Valid operators are `+, -, *, /`. Each operand may be an integer or another expression.

**Some examples:**

```
  ["2", "1", "+", "3", "*"] -> ((2 + 1) * 3) -> 9
  ["4", "13", "5", "/", "+"] -> (4 + (13 / 5)) -> 6
```

## Solutions

* C++1
```
int evalRPN(vector<string>& tokens) {
    stack<int> sta;
    for(string token : tokens)
    {
        if(token == "+" || token == "-" || token == "*" || token == "/")
        {
            int b = sta.top();
            sta.pop();
            int a = sta.top();
            sta.pop();
            if(token == "/") sta.push(a/b);
            else if(token == "*") sta.push(a*b);
            else if(token == "-") sta.push(a-b);
            else sta.push(a+b);
        }
        else
            sta.push(stoi(token));
    }
    return sta.top();
}
```

## Explanation

Using a `stack` to store integers. When found a operator, `pop` out two integers from the `stack`, execute the operation and `push` the `result` into the `stack`

* **worst-case time complexity:** O(N), where `N` is the size of the input vector `tokens`.
* **worst-case space complexity:** O(N), where `N` is the size of the input vector `tokens`.