# Defanging an IP Address

## Solution 1

StringBuilder

```java
/**
 * Question   : 1108. Defanging an IP Address
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : string
 */
class Solution {
    public String defangIPaddr(String address) {
        if (address == null || address.length() == 0) {
            return "";
        }

        StringBuilder sb = new StringBuilder();

        for (int i = 0; i < address.length(); i++) {
            char c = address.charAt(i);
            if (c != '.') {
                sb.append(c);
                continue;
            }
            sb.append("[.]");
        }

        return sb.toString();
    }
}
```
