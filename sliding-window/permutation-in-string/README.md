# Permutation in String

## Solution 1

Sliding Window

```java
/**
 * Question   : 567. Permutation in String
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Sliding Window
 */
class Solution {
    public boolean checkInclusion(String s1, String s2) {
        int[] need = new int[26];

        int require = 0;

        for (Character c : s1.toCharArray()) {
            if (need[c - 'a'] == 0) {
                require++;
            }
            need[c - 'a']++;
        }

        int left = 0;
        int right = 0;
        int[] window = new int[26];

        while (right < s2.length()) {
            char c = s2.charAt(right++);

            if (need[c - 'a'] > 0) {
                window[c - 'a']++;
                if (window[c - 'a'] == need[c - 'a']) {
                    require--;
                }
            }

            while (require == 0) {
                if (right - left == s1.length()) {
                    return true;
                }
                char charToRemove = s2.charAt(left++);
                if (need[charToRemove - 'a'] > 0) {
                    if (window[charToRemove - 'a'] == need[charToRemove - 'a']) {
                        require++;
                    }
                    window[charToRemove - 'a']--;
                }
            }
        }

        return false;
    }
}
```
