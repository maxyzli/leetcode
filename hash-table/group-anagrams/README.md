# Group Anagrams

## Solution 1

Sort

```java
/**
 * Question   : 49. Group Anagrams
 * Topics     : Hash Table
 * Complexity : Time: O(n*mlog(m)) ; Space: O(m)
 */
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> mapping = new HashMap<>();

        for (int i = 0; i < strs.length; i++) {
            String str = strs[i];
            String key = getHashCode(str);
            mapping.putIfAbsent(key, new LinkedList<>());
            mapping.get(key).add(str);
        }

        List<List<String>> res = new LinkedList<>();
        for (Map.Entry<String, List<String>> entry : mapping.entrySet()) {
            res.add(entry.getValue());
        }

        return res;
    }

    private String getHashCode(String str) {
        char[] chars = str.toCharArray();
        Arrays.sort(chars);
        return String.valueOf(chars);
    }
}
```

# Solution 2

Count Array

```java
/**
 * Question   : 49. Group Anagrams
 * Topics     : Hash Table
 * Complexity : Time: O(m*n) ; Space: O(m)
 */
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> mapping = new HashMap<>();

        for (int i = 0; i < strs.length; i++) {
            String str = strs[i];
            String key = getHashCode(str);
            mapping.putIfAbsent(key, new LinkedList<>());
            mapping.get(key).add(str);
        }

        List<List<String>> res = new LinkedList<>();
        for (Map.Entry<String, List<String>> entry : mapping.entrySet()) {
            res.add(entry.getValue());
        }

        return res;
    }

    private String getHashCode(String str) {
        char[] arr = new char[26];
        for (int j = 0; j < str.length(); j++) {
            arr[str.charAt(j) - 'a']++;
        }
        return String.valueOf(arr);
    }
}
```
