# Merge Intervals

## Solution 1

```java
/**
 * Question   : 56. Merge Intervals
 * Topics     : Array
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
            int[] incomingInterval = intervals[i];

            if (temp[1] < incomingInterval[0]) { // temp in the front.
                list.add(temp);
                temp = incomingInterval;
            } else { // Overlapping
                temp[1] = Math.max(temp[1], incomingInterval[1]);
            }
        }
        list.add(temp);

        return list.toArray(new int[list.size()][]);
    }
}
```
