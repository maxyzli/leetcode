# Insert Interval

# Solution 1

```java
/**
 * Question   : 57. Insert Interval
 * Topics     : Array
 * Complexity : Time: O(n) ; Space: O(1)
 */
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        if (intervals == null || intervals.length == 0) {
            return new int[][]{newInterval};
        }

        List<int[]> mergedList = new ArrayList<>();

        int[] temp = newInterval;
        for (int i = 0; i < intervals.length; i++) {
            int[] incomingInterval = intervals[i];

            if (temp[1] < incomingInterval[0]) { // temp in the front.
                mergedList.add(temp);
                temp = incomingInterval;
            } else if (incomingInterval[1] < temp[0]) { // incomingInterval in the front.
                mergedList.add(incomingInterval);
            } else { // Overlap
                temp = new int[]{Math.min(incomingInterval[0], temp[0]), Math.max(incomingInterval[1], temp[1])};
            }
        }
        mergedList.add(temp);

        int[][] res = new int[mergedList.size()][2];
        mergedList.toArray(res);

        return res;
    }
}
```
