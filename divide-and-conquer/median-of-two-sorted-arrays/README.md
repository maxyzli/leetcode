# Median of Two Sorted Arrays

## Solution 1

Divide and Conquer

```java
/**
 * Question   : Median of two sorted arrays of different sizes
 * Complexity : Time: O(log(n)) ; Space: O(1)
 * Topics     : Divide and Conquer
 */
public class Solution {
    @Test
    public void test() {
        assertEquals(2, findMedianSortedArrays(new int[]{1, 3}, new int[]{2}), 0);
        assertEquals(2.5, findMedianSortedArrays(new int[]{1, 2}, new int[]{3, 4}), 0);
        assertEquals(3, findMedianSortedArrays(new int[]{1}, new int[]{2, 3, 4, 5}), 0);
    }

    public double findMedianSortedArrays(int[] arr1, int[] arr2) {
        int n1 = arr1.length, n2 = arr2.length;

        // We have to make sure arr1 is shorter than arr2.
        if (n1 > n2) {
            return findMedianSortedArrays(arr2, arr1);
        }

        // Notice that high is n1, not (n1 - 1);
        int low = 0, high = n1;

        while (low <= high) {
            // How many numbers we want to take as the left part of the first array.
            int cut1 = low + (high - low) / 2;
            // How many numbers we want to take as the left part of the second array.
            int cut2 = (n1 + n2) / 2 - cut1;

            int l1 = cut1 == 0 ? Integer.MIN_VALUE : arr1[cut1 - 1];
            int l2 = cut2 == 0 ? Integer.MIN_VALUE : arr2[cut2 - 1];
            int r1 = cut1 == n1 ? Integer.MAX_VALUE : arr1[cut1];
            int r2 = cut2 == n2 ? Integer.MAX_VALUE : arr2[cut2];

            if (l1 > r2) {
                high = cut1 - 1;
            } else if (l2 > r1) {
                low = cut1 + 1;
            } else {
                if ((n1 + n2) % 2 == 0) {
                    return (Math.max(l1, l2) + Math.min(r1, r2)) / 2.0;
                } else {
                    return Math.min(r1, r2);
                }
            }
        }

        return -1;
    }
}
```

## Solution 2

Heap

```java
/**
 * Question   : 4. Median of Two Sorted Arrays
 * Complexity : Time: O(mlog(m) + nlog(n)) ; Space: O(m + n)
 * Topics     : Divide and Conquer
 */
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        MedianFinder medianFinder = new MedianFinder();

        for (int num : nums1) {
            medianFinder.addNum(num);
        }
        for (int num : nums2) {
            medianFinder.addNum(num);
        }

        return medianFinder.findMedian();
    }
}

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
