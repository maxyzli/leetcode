# Top K Frequent Elements

# Solution 1

Heap

```java
/**
 * Question   : 347. Top K Frequent Elements
 * Complexity : Time: O(nlog(k)) ; Space: O(n)
 * Topics     : Heap
 */
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        if (k > nums.length) {
            return new int[]{};
        }

        Map<Integer, Integer> count = new HashMap<>();
        for (int num : nums) {
            count.put(num, count.getOrDefault(num, 0) + 1);
        }

        PriorityQueue<Integer> pq = new PriorityQueue<>((a, b) -> count.get(a) - count.get(b));
        for (int num : count.keySet()) {
            pq.add(num);
            if (pq.size() > k) {
                pq.remove();
            }
        }

        int[] res = new int[k];
        int j = 0;
        while (!pq.isEmpty()) {
            res[j++] = pq.remove();
        }

        return res;
    }
}
```
