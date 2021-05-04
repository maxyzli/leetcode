# Can Place Flowers

## Solution 1

```java
/**
 * Question   : 605. Can Place Flowers
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        int i = 0;

        while (i < flowerbed.length && n > 0) {
            if (flowerbed[i] == 1) {
                i += 2;
            } else {
                // flowerbed[i] == 0;
                if (i == flowerbed.length - 1 || flowerbed[i + 1] == 0) {
                    flowerbed[i] = 1;
                    n--;
                } else {
                    // flowerbed[i + 1] == 1;
                    i += 3;
                }
            }
        }

        return n == 0;
    }
}
```
