# Add to Array-Form of Integer

## Solution 1

```java
/**
 * Question   : 989. Add to Array-Form of Integer
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Math
 */
class Solution {
    public List<Integer> addToArrayForm(int[] num, int k) {
        List<Integer> list = new ArrayList<>();

        int i = num.length - 1;
        int carry = 0;
        while (i >= 0 || k > 0) {
            int sum = carry;

            if (i >= 0) {
                sum += num[i--];
            }
            if (k > 0) {
                sum += k % 10;
                k /= 10;
            }

            list.add(0, sum % 10);
            carry = sum / 10;
        }

        if (carry > 0) {
            list.add(0, carry);
        }

        return list;
    }
}
```
