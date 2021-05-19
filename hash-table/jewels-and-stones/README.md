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
