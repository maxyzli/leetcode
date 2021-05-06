# Plus One

## Solution 1

```java
/**
 * Question   : 66. Plus One
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Math
 */
class Solution {
    public int[] plusOne(int[] digits) {
        List<Integer> list = new ArrayList<>();

        int carry = 1;
        for (int i = digits.length - 1; i >= 0; i--) {
            int sum = carry;
            sum += digits[i];
            list.add(0, sum % 10);
            carry = sum / 10;
        }

        if (carry > 0) {
            list.add(0, carry);
        }
        
        int[] res = new int[list.size()];
        for (int i = 0; i < list.size(); i++) {
            res[i] = list.get(i);
        }
        
        return res;
    }
}
```
