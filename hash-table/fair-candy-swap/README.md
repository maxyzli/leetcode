# Fair Candy Swap

## Solution 1

```java
/**
 * Question   : 888. Fair Candy Swap
 * Complexity : Time: O(n+m) ; Space: O(n)
 * Topics     : Hash Table
 */
class Solution {
    public int[] fairCandySwap(int[] aliceSizes, int[] bobSizes) {
        int sumA = 0;
        for (int i = 0; i < aliceSizes.length; i++) {
            sumA += aliceSizes[i];
        }
        int sumB = 0;
        for (int i = 0; i < bobSizes.length; i++) {
            sumB += bobSizes[i];
        }

        Set<Integer> set = new HashSet<>();
        for (int i = 0; i < aliceSizes.length; i++) {
            set.add(aliceSizes[i]);
        }

        for (int i = 0; i < bobSizes.length; i++) {
            // sumA - x + y = sumB + x - y ----> x = y + (sumA - sumB) / 2
            int x = bobSizes[i] + (sumA - sumB) / 2;
            if (set.contains(x)) {
                return new int[]{x, bobSizes[i]};
            }
        }

        return new int[]{};
    }
}
```
