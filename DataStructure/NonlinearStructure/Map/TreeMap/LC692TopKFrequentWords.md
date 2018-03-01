# LC692. Top K Frequent Words

### LeetCode

## Question

Given a non-empty list of words, return the k most frequent elements.

Your answer should be sorted by frequency from highest to lowest. If two words have the same frequency, then the word with the lower alphabetical order comes first.

**Example 1:**
```
Input: ["i", "love", "leetcode", "i", "love", "coding"], k = 2
Output: ["i", "love"]
Explanation: "i" and "love" are the two most frequent words.
    Note that "i" comes before "love" due to a lower alphabetical order.
```

**Example 2:**
```
Input: ["the", "day", "is", "sunny", "the", "the", "the", "sunny", "is", "is"], k = 4
Output: ["the", "is", "sunny", "day"]
Explanation: "the", "is", "sunny" and "day" are the four most frequent words,
    with the number of occurrence being 4, 3, 2 and 1 respectively.
```

**Note:**

* You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
* Input words contain only lowercase letters.

**Follow up:** Try to solve it in O(n log k) time and O(n) extra space.

## Solutions

* Java1
```
class Solution {
    
    public List<String> topKFrequent(String[] words, int k) {
        Map<String, Integer> countWords = getCountedWords(words);
        TreeMap<Integer, List<String>> frequentWords = getFrequentWords(countWords);

        return getTopKFrequentWords(frequentWords, k);
    }
    
    private Map<String, Integer> getCountedWords(String[] words){
        Map<String, Integer> countWords = new HashMap();
        for(String word : words){
            countWords.put(word, countWords.containsKey(word) ? countWords.get(word)+1 : 1);
        }
        return countWords;
    }
    
    private TreeMap<Integer, List<String>> getFrequentWords(Map<String, Integer> countWords){
        TreeMap<Integer, List<String>> frequentWords = new TreeMap(new DescOrder());
        for(Map.Entry<String, Integer> countEntry : countWords.entrySet()){
            addFrequentWord(frequentWords, countEntry.getValue(), countEntry.getKey());
        }
        return frequentWords;
    }
    
    static class DescOrder implements Comparator<Integer> {
 
        @Override
        public int compare(Integer o1, Integer o2) {        
            return o2 - o1;
        }
    }
    
    private void addFrequentWord(TreeMap<Integer, List<String>> frequentWords, int frequent, String word){
        if(!frequentWords.containsKey(frequent))
                frequentWords.put(frequent, new ArrayList<String>());
            frequentWords.get(frequent).add(word);
    }
    
    private List<String> getTopKFrequentWords(TreeMap<Integer, List<String>> frequentWords, int k){
        List<String> result = new ArrayList<>();
        for(Map.Entry<Integer, List<String>> frequentEntry : frequentWords.entrySet()){
            List<String> group = frequentEntry.getValue();
            if(group.size() > 1)
                Collections.sort(group);
            k = getRestOfK(group, result, k);
            if(k == 0) break;
        }
        return result;
    }
    
    private int getRestOfK(List<String> group, List<String> result, int k){
        for(String word : group){
            result.add(word);
            if(--k == 0) return 0;
        }
        return k;
    }
}
```

## Explanation

1. Count the frequency of each word.
2. Map the frequency to the words.
3. In descend order, add words to the results. Only sort the word frequent `group` when needed to.

* **worst-case time complexity:** O(N log(K)), where `N` is the size of the input `words`, `K` is the input `k`. 
* **worst-case space complexity:** O(N), where `N` is the size of the input `words`.