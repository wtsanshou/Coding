# LC824. Goat Latin

### LeetCode

## Question

A sentence S is given, composed of words separated by spaces. Each word consists of lowercase and uppercase letters only.

We would like to convert the sentence to "Goat Latin" (a made-up language similar to Pig Latin.)

The rules of Goat Latin are as follows:

If a word begins with a vowel (a, e, i, o, or u), append "ma" to the end of the word.
For example, the word 'apple' becomes 'applema'.
 
If a word begins with a consonant (i.e. not a vowel), remove the first letter and append it to the end, then add "ma".
For example, the word "goat" becomes "oatgma".
 
Add one letter 'a' to the end of each word per its word index in the sentence, starting with 1.
For example, the first word gets "a" added to the end, the second word gets "aa" added to the end and so on.
Return the final sentence representing the conversion from S to Goat Latin. 

**Example 1:**
```
Input: "I speak Goat Latin"
Output: "Imaa peaksmaaa oatGmaaaa atinLmaaaaa"
```

**Example 2:**
```
Input: "The quick brown fox jumped over the lazy dog"
Output: "heTmaa uickqmaaa rownbmaaaa oxfmaaaaa umpedjmaaaaaa overmaaaaaaa hetmaaaaaaaa azylmaaaaaaaaa ogdmaaaaaaaaaa"
``` 

**Notes:**

* S contains only uppercase, lowercase and spaces. Exactly one space between each word.
* 1 <= S.length <= 150.

## Solutions

* Java1
```
class Solution {
    
    private static final String MA = "maa";
    
    public String toGoatLatin(String S) {
        if(S.isEmpty()) return S;
        String[] words = S.split(" ");
        for(int i=0; i<words.length; ++i){
            if(isVowel(words[i].charAt(0)))
                words[i] = getVowelGoatLatin(words[i], i);
            else
                words[i] = getNormalGoatLatin(words[i], i);
        }
        return getStringFrom(words);
    }
    
    private boolean isVowel(char s){
        s = Character.toLowerCase(s);
        return s=='a' || s=='e' || s=='i' || s=='o' || s=='u';
    }
    
    private String getVowelGoatLatin(String word, int n){
        return word + MA + getNofA(n);
    }
    
    private String getNormalGoatLatin(String word, int n){
        return word.substring(1) + word.charAt(0) + MA + getNofA(n);
    }

    private String getNofA(int n){
        String res = "";
        for(int i=0; i<n; ++i)
            res += "a";
        return res;
    }
    
    private String getStringFrom(String[] words){
        StringBuilder sb = new StringBuilder();
        sb.append(words[0]);
        for(int i=1; i<words.length; ++i)
            sb.append(" " + words[i]);
        return sb.toString();
    }
}
```

## Explanation

**Note:** Empty String cannot be splited.

* **worst-case time complexity:** **O(N<sup>2</sup>)**, where `N` is the number of words in the String.
* **worst-case space complexity:** **O(N<sup>2</sup>)**, where `N` is the number of words in the String.