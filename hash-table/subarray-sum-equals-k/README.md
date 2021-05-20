# Subarray Sum Equals K

## Solution 1

Brute Force

```java
/**
 * Question   : 560. Subarray Sum Equals K
 * Topics     : Hash Table
 * Complexity : Time: O(n^2) ; Space: O(1)
 */
class Solution {
    public int subarraySum(int[] nums, int k) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int count = 0;

        for (int i = 0; i < nums.length; i++) {
            int sum = 0;
            for (int j = i; j >= 0; j--) {
                sum += nums[j];
                if (sum == k) {
                    count++;
                }
            }
        }

        return count;
    }
}
```

## Solution 2

PrefixSum

```java
/**
 * Question   : 560. Subarray Sum Equals K
 * Topics     : Hash Table
 * Complexity : Time: O(n^2) ; Space: O(n)
 */
class Solution {
    public int subarraySum(int[] nums, int k) {
        int n = nums.length;

        int[] prefixSum = new int[n + 1];
        prefixSum[0] = 0;
        for (int i = 1; i <= n; i++) {
            prefixSum[i] = prefixSum[i - 1] + nums[i - 1];
        }

        int count = 0;
        for (int i = 0; i < prefixSum.length; i++) {
            for (int j = 0; j < i; j++) {
                if (prefixSum[i] - prefixSum[j] == k) {
                    count++;
                }
            }
        }

        return count;
    }
}
```

## Solution 3

PrefixSum + Hash Table

```java
/**
 * Question   : 560. Subarray Sum Equals K
 * Topics     : Hash Table
 * Complexity : Time: O(n) ; Space: O(n)
 */
class Solution {
    public int subarraySum(int[] nums, int k) {
        int n = nums.length;

        int[] prefixSum = new int[n + 1];
        prefixSum[0] = 0;
        for (int i = 1; i <= n; i++) {
            prefixSum[i] = prefixSum[i - 1] + nums[i - 1];
        }

        Map<Integer, Integer> map = new HashMap<>();

        int count = 0;
        for (int i = 0; i < prefixSum.length; i++) {
            // prefixSum[i] - prefixSum[j] == k
            // => prefixSum[j] = prefixSum[i] - k
            int diff = prefixSum[i] - k;
            if (map.containsKey(diff)) {
                count += map.get(diff);
            }
            map.put(prefixSum[i], map.getOrDefault(prefixSum[i], 0) + 1);
        }

        return count;
    }
}
```

## Solution 4

PrefixSum + Hash Table + State Compression

```java
/**
 * Question   : 560. Subarray Sum Equals K
 * Topics     : Hash Table
 * Complexity : Time: O(n) ; Space: O(1)
 */
class Solution {
    public int subarraySum(int[] nums, int k) {
        int n = nums.length;

        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, 1);

        int prefixSum = 0;
        int count = 0;
        
        for (int i = 0; i < nums.length; i++) {
            // prefixSum[i] - prefixSum[j] == k
            // => prefixSum[j] = prefixSum[i] - k
            prefixSum += nums[i];
            int diff = prefixSum - k;
            if (map.containsKey(diff)) {
                count += map.get(diff);
            }
            map.put(prefixSum, map.getOrDefault(prefixSum, 0) + 1);
        }

        return count;
    }
}
```
