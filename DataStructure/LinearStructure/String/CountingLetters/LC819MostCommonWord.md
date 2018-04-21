# LC819. Most Common Word

### LeetCode

## Question

Given a paragraph and a list of banned words, return the most frequent word that is not in the list of banned words.  It is guaranteed there is at least one word that isn't banned, and that the answer is unique.

Words in the list of banned words are given in lowercase, and free of punctuation.  Words in the paragraph are not case sensitive.  The answer is in lowercase.

**Example:**
```
Input: 
paragraph = "Bob hit a ball, the hit BALL flew far after it was hit."
banned = ["hit"]
Output: "ball"
Explanation: 
"hit" occurs 3 times, but it is a banned word.
"ball" occurs twice (and no other word does), so it is the most frequent non-banned word in the paragraph. 
Note that words in the paragraph are not case sensitive,
that punctuation is ignored (even if adjacent to words, such as "ball,"), 
and that "hit" isn't the answer even though it occurs more because it is banned.
```

**Note:**

* 1 <= paragraph.length <= 1000.
* 1 <= banned.length <= 100.
* 1 <= banned[i].length <= 10.
* The answer is unique, and written in lowercase (even if its occurrences in paragraph may have uppercase symbols, and even if it is a proper noun.)
* paragraph only consists of letters, spaces, or the punctuation symbols !?',;.
* Different words in paragraph are always separated by a space.
* There are no hyphens or hyphenated words.
* Words only consist of letters, never apostrophes or other punctuation symbols.

## Solutions

* Java1
```
class Solution {
    public String mostCommonWord(String paragraph, String[] banned) {
        Set<String> ban = new HashSet();
        Map<String, Integer> wordMap = new HashMap();
        for(String word : banned){
            ban.add(word);
        }
        
        String[] words = paragraph.split(" ");
        for(String word : words){
            String target = getRealWord(word);
            if(!ban.contains(target)){
                wordMap.put(target, wordMap.containsKey(target) ? wordMap.get(target)+1 : 1);
            }
        }
        
        String result = "";
        int max = 0;
        for(Map.Entry<String, Integer> word : wordMap.entrySet()){
            if(word.getValue() > max){
                result = word.getKey();
                max = word.getValue();
            }
        }
        
        return result;
    }
    
    private String getRealWord(String word){
        int first = 0;
        int last = word.length()-1;
        for(int i=0; i< last+1; ++i){
            if(Character.isLetter(word.charAt(i))){
                first = i;
                break;
            }
        }
        
        for(int i=last; i>=0; --i){
            if(Character.isLetter(word.charAt(i))){
                last = i;
                break;
            }
        }
        return word.substring(first, last + 1).toLowerCase();
    }
}
```

## Explanation

Count the words in the paragraph which are not banned. Find the most frequent word.

The corner case is to remove all leading or tailing punctuation symbols.

* **worst-case time complexity:** `O(n + m)`, where n is the number of words in the paragraph, m is the length of the banned.
* **worst-case space complexity:** `O(n + m)`, where n is the number of words in the paragraph, m is the length of the banned.
