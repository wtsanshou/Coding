# Lint03. Anagram

### LintCode

## Question

Use Map Reduce to find anagrams in a given list of words.

**Example 1:**
```
Input: 
"lint lint lnit ln"

Output: 
  ["lint", "lint", "lnit"]
  ["ln"]
```

**Example 2:**
```
Input: 
"ab ba cab"

Output:
  ["ab", "ba"]
  ["cab"]
```

## Solutions

### Solution 1

* Java
```
/**
 * Definition of OutputCollector:
 * class OutputCollector<K, V> {
 *     public void collect(K key, V value);
 *         // Adds a key/value pair to the output buffer
 * }
 */
public class Anagram {

    public static class Map {
        public void map(String key, String value,
                        OutputCollector<String, String> output) {
            // Write your code here
            // Output the results into output buffer.
            // Ps. output.collect(String key, String value);
            String[] words = value.split(" ");
            for (String word : words) {
                String sortedWord = sort(word);
                output.collect(sortedWord, word);
            }
        }
    }
    
    private static String sort(String word) {
        char[] chars = word.toCharArray();
        Arrays.sort(chars);
        return new String(chars);
    }

    public static class Reduce {
        public void reduce(String key, Iterator<String> values,
                           OutputCollector<String, List<String>> output) {
            // Write your code here
            // Output the results into output buffer.
            // Ps. output.collect(String key, List<String> value);
            List<String> words = new LinkedList<>();
            while (values.hasNext()) {
                words.add(values.next());
            }
            output.collect(key, words);
        }
    }
}
```

#### Map

Map all words in the content of the `Document value` to the sorted word of them.

* `key`: sorted word
* `value`: original word

**Complexity:**

* **worst-case time complexity:** `O(n * w * log(w))`, where `n` is the number of word in the  `value`, `w` is the maximum length of the words.
* **worst-case space complexity:** `O(n)`, where `n` is the number of word in the  `value`.

#### Reduce

Collect all original words of a key (sorted word).

* key: sorted word
* value: list of original words

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the number of values in the iterator `values`.
* **worst-case space complexity:** `O(n)`, where `n` is the number of values in the iterator `values`.
