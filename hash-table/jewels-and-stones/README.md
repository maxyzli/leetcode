# Jewels and Stones

## Solution 1

```java
/**
 * Question   : 771. Jewels and Stones
 * Complexity : Time: O(n+m) ; Space: O(m)
 * Topics     : Hash Table
 */
class Solution {
    public int numJewelsInStones(String jewels, String stones) {
        Set<Character> set = new HashSet<>();
        
        for (int i = 0; i < jewels.length(); i++) {
            set.add(jewels.charAt(i));
        }
        
        int count = 0;
        for (int i = 0; i < stones.length(); i++) {
            if (set.contains(stones.charAt(i))) {
                count++;
            }
        }
        
        return count;
    }
}
```

## Solution 2

```java
/**
 * Question   : 771. Jewels and Stones
 * Complexity : Time: O(m+n) ; Space: O(1)
 * Topics     : Hash Table
 */
class Solution {
    public int numJewelsInStones(String jewels, String stones) {
        boolean[] set = new boolean[58];

        for (int i = 0; i < jewels.length(); i++) {
            set[jewels.charAt(i) - 'A'] = true; 
        }

        int count = 0;
        for (int i = 0; i < stones.length(); i++) {
            if (set[stones.charAt(i) - 'A']) {
                count++;
            }
        }

        return count;
    }
}
```
