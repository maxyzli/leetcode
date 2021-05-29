# K Closest Points to Origin

## Solution 1

Heap

```java
/**
 * Question   : K Closest Points to Origin
 * Complexity : Time: O(nlog(k)) ; Space: O(k)
 * Topics     : Heap
 */
public class Solution {
    public int[][] kClosest(int[][] points, int k) {
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> compareDistance(b, a));

        for (int i = 0; i < points.length; i++) {
            pq.add(points[i]);
            if (pq.size() > k) {
                pq.remove();
            }
        }

        int[][] res = new int[k][2];
        int i = 0;
        while (i < k) {
            res[i++] = pq.remove();
        }

        return res;
    }

    private int compareDistance(int[] x, int[] y) {
        int deltaX = x[0] * x[0] + x[1] * x[1];
        int deltaY = y[0] * y[0] + y[1] * y[1];
        return deltaX - deltaY;
    }
}
```
