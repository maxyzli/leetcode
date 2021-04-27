# Find Common Characters

## Solution 1

```java
import java.util.*;

/**
 * Question   : 1002. Find Common Characters
 * Complexity : Time: O(m*n) ; Space: O(1)
 * Topics     : String
 */
class Solution {
    public List<String> commonChars(String[] A) {
        if (A == null || A.length == 0) {
            return new ArrayList<>();
        }

        int[] minFreq = new int[26];

        // O(m)
        for (int i = 0; i < A[0].length(); i++) {
            int index = A[0].charAt(i) - 'a';
            minFreq[index]++;
        }

        // O(m*n)
        for (int i = 1; i < A.length; i++) { // O(n)
            int[] freq = new int[26];

            // O(m)
            for (int j = 0; j < A[i].length(); j++) {
                freq[A[i].charAt(j) - 'a']++;
            }

            // O(1)
            for (int k = 0; k < 26; k++) {
                minFreq[k] = Math.min(minFreq[k], freq[k]);
            }
        }

        List<String> list = new ArrayList<>();

        for (int i = 0; i < 26; i++) {
            for (int j = 0; j < minFreq[i]; j++) {
                list.add(String.valueOf((char) (i + 'a')));
            }
        }

        return list;
    }
}
```