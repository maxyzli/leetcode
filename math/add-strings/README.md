# Add Strings

## Solution 1

```java
/**
 * Question   : 415. Add Strings
 * Complexity : Time: O(m+n) ; Space: O(m+n)
 * Topics     : String
 */
public class Solution {
    public String addStrings(String num1, String num2) {
        StringBuilder sb = new StringBuilder();

        int i = num1.length() - 1;
        int j = num2.length() - 1;

        int carry = 0;

        while (i >= 0 || j >= 0) {
            int first = 0, second = 0;

            if (i >= 0) {
                first = num1.charAt(i) - '0';
                i--;
            }
            if (j >= 0) {
                second = num2.charAt(j) - '0';
                j--;
            }

            int sum = first + second + carry;

            carry = sum / 10;
            sb.append(sum % 10);
        }
        
        if (carry > 0) {
            sb.append(carry);
        }

        return sb.reverse().toString();
    }
}
```
