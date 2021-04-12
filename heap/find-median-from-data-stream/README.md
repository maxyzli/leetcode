# Find Median from Data Stream

## Solution 1

```java
import org.junit.Test;

import java.util.PriorityQueue;

/**
 * Question   : 295. Find Median from Data Stream
 * Topics     : Heap
 */
class MedianFinder {
    PriorityQueue<Integer> maxHeap;
    PriorityQueue<Integer> minHeap;

    public MedianFinder() {
        // We divide the numbers into two part.
        // Left (maxHeap) and Right (minHeap)
        // (1,2,3) - (4,5,6)
        maxHeap = new PriorityQueue<>((a, b) -> b - a);
        minHeap = new PriorityQueue<>();
    }

    public void addNum(int num) {
        // If maxHeap is empty, it means we don't have any number yet.
        if (maxHeap.isEmpty()) {
            maxHeap.add(num);
            return;
        }

        // If num is bigger than the max value of maxHeap,
        // it means it should put the right part.
        if (maxHeap.peek() < num) {
            minHeap.add(num);
        } else {
            // If num is smaller than the max value of maxHeap,
            // it means it should put the left part.
            maxHeap.add(num);
        }

        // Make sure the balance.
        if (maxHeap.size() - minHeap.size() > 1) {
            minHeap.add(maxHeap.remove());
        }
        if (minHeap.size() - maxHeap.size() > 1) {
            maxHeap.add(minHeap.remove());
        }
    }

    public double findMedian() {
        if (maxHeap.size() == minHeap.size()) {
            return (maxHeap.peek() + minHeap.peek()) / 2.0;
        }
        if (maxHeap.size() > minHeap.size()) {
            return maxHeap.peek();
        } else {
            return minHeap.peek();
        }
    }
}
```
