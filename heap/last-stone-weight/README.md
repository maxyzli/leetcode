# Last Stone Weight

## Solution 1

```java
/**
 * Question   : 1046. Last Stone Weight
 * Complexity : Time: O(nlog(n)) ; Space: O(n)
 * Topics     : Heap
 */
class Solution {
    public int lastStoneWeight(int[] stones) {
        PriorityQueue<Integer> pq = new PriorityQueue<>((a, b) -> b - a);
        for (int stone : stones) {
            pq.add(stone);
        }

        while (pq.size() >= 2) {
            int y = pq.remove();
            int x = pq.remove();
            if (x != y) {
                pq.add(y - x);
            }
        }

        return pq.size() == 0 ? 0 : pq.remove();
    }
}
```
