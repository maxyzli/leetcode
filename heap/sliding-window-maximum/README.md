# Sliding Window Maximum

## Solution 1

Heap with fixed size (Time Limit Exceeded)

```java
/**
 * Question   : 239. Sliding Window Maximum
 * Complexity : Time: O(nk) ; Space: O(k)
 * Topics     : Heap
 */
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        PriorityQueue<Integer> pq = new PriorityQueue<>((a, b) -> nums[b] - nums[a]);

        List<Integer> list = new ArrayList<>();

        for (int i = 0; i < k; i++) {
            pq.add(i);
        }

        list.add(nums[pq.peek()]);

        for (int i = k; i < nums.length; i++) {
            pq.add(i);
            int idxToRemove = i - k;
            pq.remove(idxToRemove);
            list.add(nums[pq.peek()]);
        }

        int[] res = new int[list.size()];
        for (int i = 0; i < list.size(); i++) {
            res[i] = list.get(i);
        }

        return res;
    }
}
```

## Solution 2

Heap without fixed size

```java
/**
 * Question   : 239. Sliding Window Maximum
 * Complexity : Time: O(nlog(n)) ; Space: O(n)
 * Topics     : Heap
 */
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        PriorityQueue<Integer> pq = new PriorityQueue<>((a, b) -> nums[b] - nums[a]);

        List<Integer> list = new ArrayList<>();

        for (int i = 0; i < k; i++) {
            pq.add(i);
        }

        list.add(nums[pq.peek()]);

        for (int i = k; i < nums.length; i++) {
            pq.add(i);
            int minAllowIdx = i - k + 1;
            while (!pq.isEmpty() && minAllowIdx > pq.peek()) {
                pq.remove();
            }
            list.add(nums[pq.peek()]);
        }

        int[] res = new int[list.size()];
        for (int i = 0; i < list.size(); i++) {
            res[i] = list.get(i);
        }

        return res;
    }
}
```

## Solution 3

Deque

```java
/**
 * Question   : 239. Sliding Window Maximum
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Heap
 */
public class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        if (nums == null || k <= 0) {
            return new int[0];
        }

        int n = nums.length;
        List<Integer> list = new ArrayList<>();

        Deque<Integer> deque = new ArrayDeque<>();

        for (int i = 0; i < nums.length; i++) {
            // remove numbers out of range k
            int minAllowIdx = i - k + 1;
            while (!deque.isEmpty() && deque.peekFirst() < minAllowIdx) {
                deque.removeFirst();
            }

            // remove smaller numbers in k range
            while (!deque.isEmpty() && nums[deque.peekLast()] <= nums[i]) {
                deque.removeLast();
            }
            deque.addLast(i);

            // Start
            if (i >= k - 1) {
                list.add(nums[deque.peekFirst()]);
            }
        }

        int[] res = new int[list.size()];
        for (int i = 0; i < list.size(); i++) {
            res[i] = list.get(i);
        }

        return res;
    }
}
```
