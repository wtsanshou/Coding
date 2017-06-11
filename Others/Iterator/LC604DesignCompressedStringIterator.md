# LC604. Design Compressed String Iterator 

### LeetCode

## Question

Design and implement a data structure for a compressed string iterator. It should support the following operations: **next** and **hasNext**.

The given compressed string will be in the form of each letter followed by a positive integer representing the number of this letter existing in the original uncompressed string.

`next()` - if the original string still has uncompressed characters, return the next letter; Otherwise return a white space.

`hasNext()` - Judge whether there is any letter needs to be uncompressed.

**Note:**

Please remember to **RESET** your class variables declared in StringIterator, as static/class variables are persisted across multiple test cases. Please see here for more details.

**Example:**
```
StringIterator iterator = new StringIterator("L1e2t1C1o1d1e1");

iterator.next(); // return 'L'
iterator.next(); // return 'e'
iterator.next(); // return 'e'
iterator.next(); // return 't'
iterator.next(); // return 'C'
iterator.next(); // return 'o'
iterator.next(); // return 'd'
iterator.hasNext(); // return true
iterator.next(); // return 'e'
iterator.hasNext(); // return false
iterator.next(); // return ' '
```

## Solutions

* C++1
```
class StringIterator {
    
private:
    vector<int> str;
    int cur;
    int len;
    
public:

    vector<int> Parse(string cs)
    {
        vector<int> res;
        int count=0;
        for(int i=0; i<cs.length(); ++i)
        {
            if(isdigit(cs[i]))
            {
                count = 10*count + (cs[i]-'0');
                if(i+1==cs.length() || !isdigit(cs[i+1]))
                {
                    res.push_back(count);
                    count=0;
                }
            }
            else
                res.push_back(cs[i]);
        }
        return res;
    }
    
    StringIterator(string compressedString) {
        str = Parse(compressedString);
        cur = 0;
        len = str.size();
    }
    
    char next() {
        if(hasNext()){
            char res = str[cur];
            if(--str[cur+1] == 0) 
                cur += 2;
            return res;
        } 
        return ' ';
    }
    
    bool hasNext() {
        return cur < len;
    }
};

/**
 * Your StringIterator object will be instantiated and called as such:
 * StringIterator obj = new StringIterator(compressedString);
 * char param_1 = obj.next();
 * bool param_2 = obj.hasNext();
 */
```

## Explanation

Parse the string to an array.

Check the `next()` in every two positions of the array.