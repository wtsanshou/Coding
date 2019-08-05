# Lint504. Inverted Index

### LintCode

## Question

Use map reduce to build inverted index for given documents.

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
 * Definition of Document:
 * class Document {
 *     public int id;
 *     public String content;
 * }
 */
public class InvertedIndex {

    public static class Map {
        public void map(String _, Document value,
                        OutputCollector<String, Integer> output) {
            // Write your code here
            // Output the results into output buffer.
            // Ps. output.collect(String key, int value);
            String[] keys = value.content.split("\\s+");
            for (String key : keys) {
                // if (!key.isEmpty())
                output.collect(key, value.id);
            }
        }
    }

    public static class Reduce {
        public void reduce(String key, Iterator<Integer> values,
                           OutputCollector<String, List<Integer>> output) {
            // Write your code here
            // Output the results into output buffer.
            // Ps. output.collect(String key, List<Integer> value);
            List<Integer> v = new ArrayList<>();
            int previous = -1;
            while (values.hasNext()) {
                int cur = values.next();
                if (cur != previous) {
                    previous = cur;
                    v.add(cur);
                }
            }
            
            output.collect(key, v);
        }
    }
}
```

#### Map

Map all words in the content of the `Document value` to the id of `Document value`

* `key`: word
* `value`: value.id

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the number of word in the  `value`.
* **worst-case space complexity:** `O(n)`, where `n` is the number of word in the  `value`.

#### Reduce

Collect all `id` of a key (word). Note the id could have duplicates.

* key: word
* value: list of `id`

**Complexity:**

* **worst-case time complexity:** `O(n)`, where `n` is the number of values in the iterator `values`.
* **worst-case space complexity:** `O(n)`, where `n` is the number of values in the iterator `values`.