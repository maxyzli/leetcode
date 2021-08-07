# Binary Watch

## Solution 1

DFS

```java
class Solution {
    public List<String> readBinaryWatch(int turnedOn) {
        int[] nums1 = {8, 4, 2, 1};
        int[] nums2 = {32, 16, 8, 4, 2, 1};
        
        List<String> res = new LinkedList<>();
        
        for (int i = 0; i <= turnedOn; i++) {
            List<Integer> hours = findCombinations(nums1, i);
            List<Integer> minutes = findCombinations(nums2, turnedOn - i);
            
            for (int hour : hours) {
                if (hour > 11) {
                    continue;
                }
                for (int minute : minutes) {
                    if (minute > 59) {
                        continue;
                    }
                    String minuteStr = minute < 10 ? "0" + minute : minute + "";
                    res.add(hour + ":" + minuteStr);
                }
            }
        }
        
        return res;
    }
    
    private List<Integer> findCombinations(int[] nums, int k) {
        if (nums == null || nums.length == 0) {
            return new LinkedList<>();
        }
            
        List<Integer> res = new LinkedList<>();
        int index = 0;
        int curr = 0;
        dfs(nums, index, k, curr, res);
        return res;
    }
    
    private void dfs(int[] nums, int start, int k, int curr, List<Integer> res) {
        if (start >= nums.length || k == 0) {
            if (k == 0) {
                res.add(curr);
            }
            return;
        }
        
        for (int i = start; i < nums.length; i++) {
            dfs(nums, i + 1, k - 1, curr + nums[i], res);
        }
    }
}
```
