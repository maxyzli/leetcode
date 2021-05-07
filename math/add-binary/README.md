# Add Binary

## Solution 1

```java
/**
 * Question   : 67. Add Binary
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Math
 */
class Solution {
    public String addBinary(String a, String b) {
        StringBuilder sb = new StringBuilder();

        int carry = 0;
        int i = a.length() - 1;
        int j = b.length() - 1;

        while (i >= 0 || j >= 0) {
            int sum = carry;

            if (i >= 0) {
                sum += a.charAt(i) - '0';
                i--;
            }
            if (j >= 0) {
                sum += b.charAt(j) - '0';
                j--;
            }

            sb.append(sum % 2);
            carry = sum / 2;
        }

        if (carry > 0) {
            sb.append(carry);
        }

        return sb.reverse().toString();
    }
}
```
