# Minimum Swaps to Group All 1's Together

## Solution 1

Sliding Window

```java
/**
 * Question   : 1151. Minimum Swaps to Group All 1's Together
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Sliding Window
 */
class Solution {
    public int minSwaps(int[] data) {
        if (data == null || data.length == 0) {
            return 0;
        }

        int k = 0;
        for (int i = 0; i < data.length; i++) {
            if (data[i] == 1) {
                k++;
            }
        }

        int left = 0;
        int right = 0;
        int windowZeroCount = 0;
        int minZeroCount = Integer.MAX_VALUE;

        while (right < data.length) {
            int number = data[right++];

            if (number == 0) {
                windowZeroCount++;
            }

            if (right - left == k) {
                minZeroCount = Math.min(minZeroCount, windowZeroCount);
                int numberToRemove = data[left++];
                if (numberToRemove == 0) {
                    windowZeroCount--;

                }
            }
        }

        return minZeroCount == Integer.MAX_VALUE ? 0 : minZeroCount;
    }
}
```
