# Kth Largest Element in an Array

## Solution 1

Brute Force

```java
class Solution {
	public int findKthLargest(int[] nums, int k) {
	    Arrays.sort(nums);
	    return nums[nums.length-k];
	}
}
```

## Solution 2

Heap

```java
/**
 * Question   : 215. Kth Largest Element in an Array
 * Complexity : Time: O(nlog(k)) ; Space: O(1)
 * Topics     : Heap
 * Date       : 2021/03/11
 */
class Solution {
    public int findKthLargest(int[] arr, int k) {
        if (arr == null || arr.length == 0) {
            return 0;
        }

        PriorityQueue<Integer> pq = new PriorityQueue<>();

        for (int i = 0; i < k; i++) {
            pq.add(arr[i]);
        }

        for (int i = k; i < arr.length; i++) {
            if (pq.peek() < arr[i]) {
                pq.remove();
                pq.add(arr[i]);
            }
        }

        return pq.remove();
    }
}
```
