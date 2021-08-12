# Subsets II

## Solution 1

```java
/**
 * Question   : 90. Subsets II
 * Complexity : Time: O(2^n) ; Space: O(n)
 * Topics     : Backtracking
 */
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        if (nums == null || nums.length == 0) {
            return new LinkedList<>();
        }
        
        Arrays.sort(nums);
        List<List<Integer>> res = new LinkedList<>();
        List<Integer> list = new LinkedList<>();
        int startIdx = 0;
        
        dfs(nums, startIdx, list, res);
        
        return res;
    }
    
    private void dfs(int[] nums, int startIdx, List<Integer> list, List<List<Integer>> res) {
        res.add(new LinkedList<>(list));
        
        for (int i = startIdx; i < nums.length; i++) {
            if (i != startIdx && nums[i - 1] == nums[i]) {
                continue;
            }
            list.add(nums[i]);
            dfs(nums, i + 1, list, res);
            list.remove(list.size() - 1);
        }
    }
}
```
