# 3Sum

## Solution 1

Recursion

```java
/**
 * Question   : 15. 3Sum
 * Complexity : Time: O(n^2) ; Space: O(n)
 * Topics     : array
 */
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        if (nums == null || nums.length == 0) {
            return new ArrayList<>();
        }
        Arrays.sort(nums);
        return threeSum(nums, 0);
    }

    private List<List<Integer>> threeSum(int[] nums, int target) {
        int n = nums.length;

        List<List<Integer>> res = new ArrayList<>();

        int i = 0;
        while (i < n) {
            int num = nums[i];

            List<List<Integer>> twoSumList = twoSum(nums, i + 1, target - num);

            if (!twoSumList.isEmpty()) {
                for (int j = 0; j < twoSumList.size(); j++) {
                    List<Integer> temp = new ArrayList<>();
                    temp.add(num);
                    temp.addAll(twoSumList.get(j));
                    res.add(temp);
                }
            }

            // Remove n1 duplicate.
            while (i < n && nums[i] == num) {
                i++;
            }
        }

        return res;
    }

    private List<List<Integer>> twoSum(int[] nums, int start, int target) {
        int n = nums.length;
        int low = start;
        int high = n - 1;

        List<List<Integer>> res = new ArrayList<>();

        while (low < high) {
            int num1 = nums[low];
            int num2 = nums[high];

            if (num1 + num2 == target) {
                res.add(Arrays.asList(num1, num2));
                // Remove n2 duplicate.
                while (low < high && nums[low] == num1) {
                    low++;
                }
                // Remove n3 duplicate.
                while (low < high && nums[high] == num2) {
                    high--;
                }
            } else if (num1 + num2 < target) {
                while (low < high && nums[low] == num1) {
                    low++;
                }
            } else {
                while (low < high && nums[high] == num2) {
                    high--;
                }
            }
        }

        return res;
    }
}
```
