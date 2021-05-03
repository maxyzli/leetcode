# Pascal's Triangle II

## Solution 1

Space: O(n^2)

```java
/**
 * Question   : 119. Pascal's Triangle II
 * Complexity : Time: O(n) ; Space: O(n^2)
 * Topics     : Array
 */
class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<List<Integer>> res = new ArrayList<>();

        for (int currRow = 0; currRow <= rowIndex; currRow++) {
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

        return res.get(rowIndex);
    }
}
```

## Solution 2

Space: O(n)

```java
/**
 * Question   : 119. Pascal's Triangle II
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Array
 */
class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<Integer> preRow = new ArrayList<>();

        for (int currRow = 0; currRow <= rowIndex; currRow++) {
            List<Integer> currList = new ArrayList<>();
            for (int col = 0; col <= currRow; col++) {
                if (col == 0 || col == currRow) {
                    currList.add(1);
                } else {
                    currList.add(preRow.get(col - 1) + preRow.get(col));
                }
            }
            preRow = currList;
        }

        return preRow;
    }
}
```

## Solution 3

```java
/**
 * Question   : 119. Pascal's Triangle II
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Array
 */
class Solution {
    public List<Integer> getRow(int rowIndex) {
        Integer[] res = new Integer[rowIndex + 1];
        Arrays.fill(res, 0);
        res[0] = 1;

        for (int row = 1; row <= rowIndex; row++) {
            for (int col = row; col > 0; col--) {
                res[col] = res[col - 1] + res[col];
            }
        }

        return Arrays.asList(res);
    }
}
```
