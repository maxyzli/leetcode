# Container With Most Water

## Solution 1

```java
/**
 * Question   : 11. Container With Most Water
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public int maxArea(int[] height) {
        int low = 0;
        int high = height.length - 1;

        int maxArea = 0;

        while (low <= high) {
            maxArea = Math.max(maxArea, Math.min(height[low], height[high]) * (high - low));
            if (height[low] < height[high]) {
                low++;
            } else {
                high--;
            }
        }

        return maxArea;
    }
}
```