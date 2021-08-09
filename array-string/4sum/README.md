# 4Sum

## Solution 1

Recursion

```java
/**
 * Question   : 4Sum
 * Complexity : Time: O(n^3) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    // [n1, n2, n3, n4]
    public static List<List<Integer>> fourSum(int[] nums, int target) {
        Arrays.sort(nums);

        int N = nums.length;

        List<List<Integer>> res = new LinkedList<>();

        int i = 0;
        while (i < N) {
            int num = nums[i];
            List<List<Integer>> sub = threeSum(nums, i + 1, target - num);

            for (List<Integer> list : sub) {
                List<Integer> temp = new LinkedList<>();
                temp.add(num);
                temp.addAll(list);
                res.add(temp);
            }

            // prevent duplicate for n1.
            while (i < N && nums[i] == num) {
                i++;
            }
        }

        return res;
    }

    public static List<List<Integer>> threeSum(int[] nums, int start, int target) {
        int N = nums.length;

        List<List<Integer>> res = new LinkedList<>();

        int i = start;
        while (i < N) {
            int num = nums[i];
            List<List<Integer>> sub = twoSum(nums, i + 1,target - num);

            for (List<Integer> list : sub) {
                List<Integer> temp = new LinkedList<>();
                temp.add(num);
                temp.addAll(list);
                res.add(temp);
            }

            // prevent duplicate for n2.
            while (i < N && nums[i] == num) {
                i++;
            }
        }

        return res;
    }

    public static List<List<Integer>> twoSum(int[] nums, int start, int target) {
        // Two Pointers
        int low = start;
        int high = nums.length - 1;

        List<List<Integer>> res = new LinkedList<>();

        while (low < high) {
            int num1 = nums[low];
            int num2 = nums[high];

            int sum = num1 + num2;

            if (sum == target) {
                res.add(Arrays.asList(num1, num2));
                // prevent duplicate for n3 and n4.
                while (low < high && nums[low] == num1) {
                    low++;
                }
                while (low < high && nums[high] == num2) {
                    high--;
                }
            } else if (sum < target) {
                // prevent duplicate for n3.
                while (low < high && nums[low] == num1) {
                    low++;
                }
            } else {
                // prevent duplicate for n4.
                while (low < high && nums[high] == num2) {
                    high--;
                }
            }
        }

        return res;
    }
}
```

## Solution 2

4 Pointers

```java
/**
 * Question   : 18. 4Sum
 * Complexity : Time: O(n^3) ; Space: O(1)
 * Topics     : array
 */
class Solution {
    public List<List<Integer>> fourSum(int[] arr, int target) {
        if (arr == null || arr.length == 0) {
            return new LinkedList<>();
        }

        Arrays.sort(arr);

        int n = arr.length;
        List<List<Integer>> res = new LinkedList<>();

        int i = 0;
        while (i < n) {
            int j = i + 1;
            while (j < n) {
                int left = j + 1;
                int right = n - 1;
                while (left < right) {
                    int sum = arr[i] + arr[j] + arr[left] + arr[right];
                    if (sum == target) {
                        res.add(Arrays.asList(arr[i], arr[j], arr[left], arr[right]));
                        // Remove duplicates.
                        int curr = arr[left];
                        while (left < n && arr[left] == curr) {
                            left++;
                        }
                        curr = arr[right];
                        while (right >= 0 && arr[right] == curr) {
                            right--;
                        }
                    } else if (sum > target) {
                        right--;
                    } else {
                        left++;
                    }
                }
                int curr = arr[j];
                while (j < n && arr[j] == curr) {
                    j++;
                }
            }
            int curr = arr[i];
            while (i < n && arr[i] == curr) {
                i++;
            }
        }

        return res;
    }
}
```
