# Lint1650. Legal Article

### LintCode

## Question

Given an article consisting of uppercase letters, lowercase letters, commas, and periods, find the number of letters that are illegal.

There are 2 situations that can cause an article to be illegal:

* The first letter of a sentence is in lowercase.
* The letter which is not the first letter of the word is in uppercase.

**Example1**
```
Input: 
s="This won iz correkt. It has, No Mistakes et Oll. But there are two BIG mistakes in this sentence. and here is one more."

Output: 3

Explanation:
The letter 'I' and 'G' in the word 'BIG' and the letter 'a' of the first word of the third sentence is incorrect.
```

**Example2**
```
input: s="Hahaha. HahaHa. hahahah."

Output: 2

The second 'H' in the word 'HahaHa' and the first 'h' in the word 'hahahah' is incorrect.
```

**Notice**

* A sentence ends if and only if it is a period.
* The length of the article does not exceed 10000.

## Solutions

### Solution 1

* Java
```
public class Solution {
    /**
     * @param s: the article
     * @return: the number of letters that are illegal
     */
    public int count(String s) {
        // Write your code here.
        int res = 0;
        String[] sentenses = s.split("\\.");
        
        for (String sentens : sentenses) {
            res += check(sentens);
        }
        
        return res;
    }
    
    private int check(String sentens) {
        sentens = sentens.trim();
        if (sentens.isEmpty()) return 0;
        
        int firstLetter = 0;
        for (; firstLetter < sentens.length(); firstLetter++) 
            if (Character.isLetter(sentens.charAt(firstLetter)))
                break;
        
        sentens = sentens.substring(firstLetter);
        
        int res = Character.isLowerCase(sentens.charAt(0)) ? 1 : 0;

        String[] words = sentens.split("[,\\s*]");
        for (int i = 0; i < words.length; i++) {
            res += illegal(words[i].trim());
        }
        return res;
    }
    
    private int illegal(String word) {
        char[] arr = word.toCharArray();
        int res = 0;
        for (int i = 1; i < arr.length; i++) 
            if (Character.isUpperCase(arr[i])) res++;
        return res;
    }
}
```

This question looks easy, but a lot of trick parts:

* Some requirements are not clear, should clarify: 

1. Spaces is consisted in the article.
2. Commas could be at the beginning of a sentence.
3. The final sentence may be no period.

**NOTE** careful read the question, it is asking for the number of **letters** that are illegal, not words, not sentences.

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the length of the input `s`.
* **worst-case space complexity:** `O(n)`, where `n` is the length of the input `s`.
