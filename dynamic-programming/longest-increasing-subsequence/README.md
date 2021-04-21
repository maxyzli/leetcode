# Longest Increasing Subsequence

## Solution 1

DFS (Time Limit Exceeded)

```java
/**
 * Question   : 300. Longest Increasing Subsequence
 * Complexity : Time: O(2^b) ; Space: O(n)
 * Topics     : DP
 */
class Solution {
    int longest;

    public int lengthOfLIS(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        longest = 0;
        List<Integer> list = new ArrayList<>();
        int beginIndex = 0;

        lengthOfLISUtil(nums, beginIndex, list);
        
        return longest;
    }

    private void lengthOfLISUtil(int[] nums, int beginIndex, List<Integer> list) {
        longest = Math.max(longest, list.size());
        
        for (int i = beginIndex; i < nums.length; i++) {
            if (list.isEmpty() || nums[i] > list.get(list.size() - 1)) {
                list.add(nums[i]);
                lengthOfLISUtil(nums, i + 1, list);
                list.remove(list.size() - 1);
            }
        }
    }
}
```

## Solution 2

DP

```java
/**
 * Question   : 300. Longest Increasing Subsequence
 * Complexity : Time: O(n^2) ; Space: O(n)
 * Topics     : DP
 */
public class Solution {
    public int lengthOfLIS(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int[] memo = new int[nums.length];
        Arrays.fill(memo, 1);

        int longest = 1;

        for (int j = 1; j < nums.length; j++) {
            for (int i = 0; i < j; i++) {
                if (nums[i] < nums[j]) {
                    memo[j] = Math.max(memo[j], memo[i] + 1);
                    longest = Math.max(longest, memo[j]);
                }
            }
        }

        return longest;
    }
}
```

## Solution 3

DP (Backword)

```java
/**
 * Question   : 300. Longest Increasing Subsequence
 * Complexity : Time: O(n^2) ; Space: O(n)
 * Topics     : DP
 */
class Solution {
    public int lengthOfLIS(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int n = nums.length;

        int[] memo = new int[n];
        Arrays.fill(memo, 1);

        int longest = 1;

        //  0   1  2  3  4  5   6    7
        // [10, 9, 2, 5, 3, 7, 101, 18]
        //            i              j
        for (int i = n - 2; i >= 0; i--) {
            for (int j = n - 1; j > i; j--) {
                if (nums[i] < nums[j]) {
                    memo[i] = Math.max(memo[i], 1 + memo[j]);
                    longest = Math.max(longest, memo[i]);
                }
            }
        }

        return longest;
    }
}
```
