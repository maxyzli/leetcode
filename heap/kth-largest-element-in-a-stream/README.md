# Kth Largest Element in a Stream

## Solution 1

Heap

```java
/**
 * Question   : 703. Kth Largest Element in a Stream
 * Complexity : Time: O(nlog(k)) ; Space: O(1)
 * Topics     : Heap
 */
class KthLargest {
    PriorityQueue<Integer> pq;
    int k;

    public KthLargest(int k, int[] nums) {
        this.pq = new PriorityQueue<>();
        this.k = k;
        for (int i = 0; i < nums.length; i++) {
            add(nums[i]);
        }
    }

    public int add(int val) {
        pq.add(val);
        if (pq.)
        return pq.peek();
    }
}
```
