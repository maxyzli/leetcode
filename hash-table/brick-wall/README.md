# Brick Wall

## Solution 1

```java
/**
 * Question   : 554. Brick Wall
 * Complexity : Time: O(m*n) ; Space: O(n)
 * Topics     : Hash Table
 */
class Solution {
    public int leastBricks(List<List<Integer>> wall) {
        // <edgeIndex, count>
        Map<Integer, Integer> edgeFreq = new HashMap<>();

        int maxFreq = 0;

        for (int i = 0; i < wall.size(); i++) {
            List<Integer> row = wall.get(i);
            // We should not consider edges of the wall.
            int edgePosition = 0;
            for (int brickIdx = 0; brickIdx < row.size() - 1; brickIdx++) {
                edgePosition += row.get(brickIdx);
                edgeFreq.put(edgePosition, edgeFreq.getOrDefault(edgePosition, 0) + 1);
                maxFreq = Math.max(maxFreq, edgeFreq.get(edgePosition));
            }
        }

        return wall.size() - maxFreq;
    }
}
```
