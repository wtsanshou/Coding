# LC227. Basic Calculator II

### LeetCode

## Question

Implement a basic calculator to evaluate a simple expression string.
The expression string contains only non-negative integers, `+, -, *, /`operators and empty spaces . The integer division should truncate toward zero.
You may assume that the given expression is always valid.

**Some examples:**

```
"3+2*2" = 7
" 3/2 " = 1
" 3+5 / 2 " = 5
```

**Note:** Do not use the eval built-in library function.

## Solutions

### Solution 1

* C++
```
int calculate(string s) {
    stack<int> nums;
    char operators = '+';
    int res=0, sign = 1;
    for(char c : s)
    {
        if(isdigit(c))
            res = res*10 + (c-'0');
        else if(c != ' ')
        {
            nums.push(sign*res);
            if(operators=='*' || operators=='/')
            {
                int b = nums.top();
                nums.pop();
                int a = nums.top();
                nums.pop();
                nums.push((operators=='*') ? a*b : a/b);
            }
            operators = c;
            if(c=='-')
                sign=-1;
            else
                sign = 1;
            res=0;
        }
    }
    res = sign*res;
    if(operators=='*' || operators=='/')
    {
        res = (operators=='*') ? nums.top()*res : nums.top()/res;
        nums.pop();
    }
    while(!nums.empty())
    {
        res += nums.top();
        nums.pop();
    }
    return res;
}
```

* C++
```
int calculate(string s) {
    stack<int>pos;
    s = s+"+";
    int num=0;
    char sign = '+';
    for(char c : s)
    {
        if(isdigit(c))
        {
            num = num*10 + (c-'0');
        }
        else if(!isspace(c))
        {
            switch(sign)
            {
                case '+': 
                    pos.push(num); 
                    break;
                case '-': 
                    pos.push(-num); 
                    break;    
                case '*': 
                    num *=pos.top();
                    pos.pop();
                    pos.push(num); 
                    break;  
                case '/': 
                    num =pos.top()/num;
                    pos.pop();
                    pos.push(num); 
                    break;  
            }
            num = 0;
            sign = c;
        }
    }
    while(!pos.empty())
    {
        num +=pos.top();
        pos.pop();
    }
    return num;
}
```

* Java
```
public int calculate(String s) {
    Deque<Integer> stack = new LinkedList<>();
    s += "+";
    char[] arr = s.toCharArray();
    int num = 0;
    char preOperator = '+';
    for (char c : arr) {
        if (Character.isDigit(c)) {
            num = num * 10 + (c - '0');
        } else if (!Character.isSpace(c)) {
            switch (preOperator) {
                case '+' :
                    stack.addFirst(num);
                    break;
                case '-' :
                    stack.addFirst(-num);
                    break;
                case '*' :
                    num *= stack.removeFirst();
                    stack.addFirst(num);
                    break;
                case '/' :
                    num = stack.removeFirst() / num;
                    stack.addFirst(num);
                    break;
                default:
                    break;
            }
            num = 0;
            preOperator = c;
        }
    }
    
    while(!stack.isEmpty())
        num += stack.removeFirst();

    return num;
}
```

The key of this question is that we have to calculate the `*` and `/` operation first. Because there are no parentheses and negative integers, we can simplify the input to a list of integers by combine the `*` and `/` into an integer of their result. Then, we can just sum the list of integers to get the final result.

To impliment the algorithm, we use a stack to store the list of integers. When previous operator is `-`, set the `num` as negative and push it to the stack; when previous operator is `*` or `/`, calculate the result and push it to the stack again. Finally, sum all integers in the stack to get the final result.

**NOTE :** Do not forget the last number in the input.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of `s`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of `s`. 
