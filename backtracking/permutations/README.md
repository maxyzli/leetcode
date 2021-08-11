# Permutations

## Solution 1

```java
/**
 * Question   : 46. Permutations
 * Complexity : Time: O(n!) ; Space: O(n)
 * Topics     : Backtracking
 */
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        if (nums == null || nums.length == 0) {
            return new LinkedList<>();
        }
        
        List<Integer> list = new LinkedList<>();
        List<List<Integer>> res = new LinkedList<>();
        boolean[] used = new boolean[nums.length];
        
        dfs(nums, used, list, res);
        
        return res;
    }
       
    private void dfs(int[] nums, boolean[] used, List<Integer> list, List<List<Integer>> res) {
        if (list.size() == nums.length) {
           res.add(new LinkedList(list));
           return;
        }
        
        for (int i = 0; i < nums.length; i++) {
            if (used[i]) {
                continue;
            }

            list.add(nums[i]);
            used[i] = true;
            
            dfs(nums, used, list, res);
            
            list.remove(list.size() - 1);
            used[i] = false;
        }
    }
}
```
