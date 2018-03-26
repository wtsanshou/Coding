# LC804. Unique Morse Code Words

### LeetCode

## Question

International Morse Code defines a standard encoding where each letter is mapped to a series of dots and dashes, as follows: "a" maps to ".-", "b" maps to "-...", "c" maps to "-.-.", and so on.

For convenience, the full table for the 26 letters of the English alphabet is given below:

`[".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."]`

Now, given a list of words, each word can be written as a concatenation of the Morse code of each letter. For example, "cab" can be written as "-.-.-....-", (which is the concatenation "-.-." + "-..." + ".-"). We'll call such a concatenation, the transformation of a word.

Return the number of different transformations among all words we have.

**Example:**
```
Input: words = ["gin", "zen", "gig", "msg"]
Output: 2
Explanation: 
The transformation of each word is:
"gin" -> "--...-."
"zen" -> "--...-."
"gig" -> "--...--."
"msg" -> "--...--."

There are 2 different transformations, "--...-." and "--...--.".
```

**Note:**

* The length of words will be at most 100.
* Each words[i] will have length in range [1, 12].
* words[i] will only consist of lowercase letters.

## Solutions

* Java1
```
class Solution {
    
    private String[] MORSE_CODE = {".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."};
    public int uniqueMorseRepresentations(String[] words) {
        Set<String> transformations = new HashSet();
        for(String word : words){
            String morse = "";
            for(int i=0; i<word.length(); ++i){
                morse += MORSE_CODE[word.charAt(i) - 'a'];
            }
            transformations.add(morse);
        }
        return transformations.size();
    }
}
```

## Explanation

`HashSet` will remove duplicate transformations.

* **worst-case time complexity:** `O(N * L)`, `N` is the number of the `words`, `L` is the length the longest word.
* **worst-case space complexity:** `O(N)`, `N` is the number of the `words`.
