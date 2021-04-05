# Valid Anagram

## Solution 1

Sorting

```java
/**
 * Question   : 242. Valid Anagram
 * Topics     : String
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
import java.util.*;

/**
 * Question   : 242. Valid Anagram
 * Topics     : String
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
