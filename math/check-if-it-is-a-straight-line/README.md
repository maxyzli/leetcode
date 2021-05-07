# Check If It Is a Straight Line

## Solution 1

```java
/**
 * Question   : 1232. Check If It Is a Straight Line
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Math
 */
public class Solution {
    public boolean checkStraightLine(int[][] coordinates) {
        int x0 = coordinates[0][0];
        int y0 = coordinates[0][1];
        int deltaX = coordinates[1][0] - x0;
        int deltaY = coordinates[1][1] - y0;

        for (int i = 2; i < coordinates.length; i++) {
            int deltaXi = coordinates[i][0] - x0;
            int deltaYi = coordinates[i][1] - y0;
            // In order to avoid being divided by 0, use multiplication form.
            // Origin: if (deltaY / deltaX != deltaYi / deltaXi)
            if (deltaXi * deltaY != deltaX * deltaYi) {
                return false;
            }
        }

        return true;
    }
}
```
