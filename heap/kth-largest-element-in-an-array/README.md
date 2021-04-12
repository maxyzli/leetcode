# Kth Largest Element in an Array

# Solution 1

Brute Force

```java
/**
 * Question   : 215. Kth Largest Element in an Array
 * Complexity : Time: O(nlog(n)) ; Space: O(n)
 * Topics     : array
 */
class Solution {
	public int findKthLargest(int[] nums, int k) {
	    Arrays.sort(nums);
	    return nums[nums.length-k];
	}
}
```

# Solution 2

Quick Select

```java
/**
 * Question   : 215. Kth Largest Element in an Array
 * Complexity : Time: O(n^2) ; Space: O(1)
 * Topics     : array
 */
class Solution {
    public int findKthLargest(int[] nums, int k) {
        if (nums == null || nums.length == 0) {
            return Integer.MIN_VALUE;
        }
        return quickSelect(nums, 0, nums.length - 1, nums.length - k);
    }

    private int quickSelect(int[] nums, int low, int high, int targetIndex) {
        if (low == high) {
            return nums[low];
        }

        int pi = partition(nums, low, high);

        if (pi == targetIndex) {
            return nums[pi];
        } else if (pi > targetIndex) {
            return quickSelect(nums, low, pi - 1, targetIndex);
        } else {
            return quickSelect(nums, pi + 1, high, targetIndex);
        }
    }

    private int partition(int[] nums, int low, int high) {
        int pivot = nums[high];

        int i = low;
        int j = low;

        while (j < high) {
            if (nums[j] < pivot) {
                swap(nums, i, j);
                i++;
            }
            j++;
        }
        swap(nums, i, high);

        return i;
    }

    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```

# Solution 3

Heap

```java
/**
 * Question   : 215. Kth Largest Element in an Array
 * Complexity : Time: O(nlog(k)) ; Space: O(1)
 * Topics     : array
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
