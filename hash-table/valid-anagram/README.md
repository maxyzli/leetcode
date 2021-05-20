# Valid Anagram

## Solution 1

Sorting

```java
/**
 * Question   : 242. Valid Anagram
 * Topics     : Hash Table
 * Complexity : Time: O(nlog(n)) ; Space: O(n)
 */
class Solution {
    public boolean isAnagram(String s, String t) {
        char[] temp = s.toCharArray();
        Arrays.sort(temp);
        String sortedS = Arrays.toString(temp);

        temp = t.toCharArray();
        Arrays.sort(temp);
        String sortedT = Arrays.toString(temp);       
        
        return sortedS.equals(sortedT);
    }
}
```

## Solution 2

Count Array

```java
/**
 * Question   : 242. Valid Anagram
 * Topics     : Hash Table
 * Complexity : Time: O(n) ; Space: O(1)
 */
class Solution {
    int[] counter = new int[26];

    public boolean isAnagram(String s, String t) {
        for (int i = 0; i < s.length(); i++) {
            counter[s.charAt(i) - 'a']++;
        }
        for (int i = 0; i < t.length(); i++) {
            counter[t.charAt(i) - 'a']--;
        }
        for (int i = 0; i < 26; i++) {
            if (counter[i] != 0) {
                return false;
            }
        }
        return true;
    }
}
```

## Solution 3

Follow up: What if the inputs contain Unicode characters? How would you adapt your solution to such a case?

```java
/**
 * Question   : 242. Valid Anagram
 * Topics     : Hash Table
 * Complexity : Time: O(n) ; Space: O(n)
 */
class Solution {

    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }
        
        Map<Character, Integer> charCount = new HashMap<>();

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            charCount.put(c, charCount.getOrDefault(c, 0) + 1);
        }

        for (int i = 0; i < t.length(); i++) {
            char c = t.charAt(i);
            charCount.put(c, charCount.getOrDefault(c, 0) - 1);
            if (charCount.get(c) < 0) {
                return false;
            }
        }

        return true;
    }
}
```
