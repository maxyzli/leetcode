# Pascal's Triangle

## Solution 1

```java
/**
 * Question   : 118. Pascal's Triangle
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public List<List<Integer>> generate(int numRows) {
        if (numRows == 0) {
            return new ArrayList<>();
        }

        List<List<Integer>> res = new ArrayList<>();

        for (int currRow = 0; currRow < numRows; currRow++) {
            List<Integer> currList = new ArrayList<>();
            for (int col = 0; col <= currRow; col++) {
                if (col == 0 || col == currRow) {
                    currList.add(1);
                } else {
                    List<Integer> preRow = res.get(currRow - 1);
                    currList.add(preRow.get(col - 1) + preRow.get(col));
                }
            }
            res.add(currList);
        }

        return res;
    }
}
```
