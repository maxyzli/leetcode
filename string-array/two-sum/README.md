# Two Sum

# Solution 1

Brute Force

```java
/**
 * Question   : 1. 2Sum
 * Complexity : Time: O(nlog(n)) ; Space: O(n)
 * Topics     : array
 */
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for (int i = 0; i < nums.length; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[i] + nums[j] == target) {
                    return new int[]{i, j};
                }
            }
        }
        return new int[]{};
    }
}
```

# Solution 2

Hash Table

```java
/**
 * Question   : 1. 2Sum
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : array
 */
class Solution {
    public int[] twoSum(int[] arr, int target) {
        HashMap<Integer, Integer> map = new HashMap<>();

        for (int i = 0; i < arr.length; i++) {
            int want = target - arr[i];
            if (map.containsKey(want)) {
                return new int[]{map.get(want), i};
            } else {
                map.put(arr[i], i);
            }
        }

        return new int[]{};
    }
}
```
