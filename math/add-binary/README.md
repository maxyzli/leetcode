# Add Binary

## Solution 1

```java
/**
 * Question   : 67. Add Binary
 * Complexity : Time: O(m+n) ; Space: O(m+n)
 * Topics     : String
 */
class Solution {
    public String addBinary(String a, String b) {
        StringBuilder sb = new StringBuilder();
        int carry = 0;
        int i = a.length() - 1;
        int j = b.length() - 1;

        while (i >= 0 && j >= 0) {
            int sum = carry;
            sum += (a.charAt(i--) - '0');
            sum += (b.charAt(j--) - '0');
            sb.insert(0, sum % 2);
            carry = sum / 2;
        }
        while (i >= 0) {
            int sum = carry;
            sum += (a.charAt(i--) - '0');
            sb.insert(0, sum % 2);
            carry = sum / 2;
        }
        while (j >= 0) {
            int sum = carry;
            sum += (b.charAt(j--) - '0');
            sb.insert(0, sum % 2);
            carry = sum / 2;
        }

        if (carry != 0) {
            sb.insert(0, carry);
        }

        return sb.toString();
    }
}
```
