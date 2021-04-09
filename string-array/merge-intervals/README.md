# Merge Intervals

## Solution 1

```java
import java.util.*;

/**
 * Question   : 56. Merge Intervals
 * Topics     : array
 * Complexity : Time: O(nlogn) ; Space: O(n)
 */
class Solution {
    public int[][] merge(int[][] intervals) {
        if (intervals == null || intervals.length <= 1) {
            return intervals;
        }

        // 1. Sorting: start ascending, end ascending
        Arrays.sort(intervals, (a, b) -> {
            if (a[0] != b[0]) {
                return a[0] - b[0];
            }
            return a[1] - b[1];
        });

        // 2. Merge Interval
        List<int[]> list = new ArrayList<>();
        int[] temp = intervals[0];

        for (int i = 1; i < intervals.length; i++) {
            int[] newInterval = intervals[i];

            // No overlap.
            if (newInterval[0] > temp[1]) {
                list.add(temp);
                temp = newInterval;
            } else {
                // Overlapping
                temp[1] = Math.max(temp[1], newInterval[1]);
            }
        }
        list.add(temp);

        return list.toArray(new int[list.size()][]);
    }
}
```
