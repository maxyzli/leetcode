# Restore IP Addresses

## Solution 1

```java
/**
 * Question   : 93. Restore IP Addresses
 * Complexity : Time: O(3^SEG_COUNT) ; Space: O(SEG_COUNT)
 * Topics     : Backtracking
 */
class Solution {
    private static final int MAX_LENGTH = 3;
    private static final int MAX_INT = 255;
    private static final int IP_SEGMENT_COUNT = 4;

    public List<String> restoreIpAddresses(String s) {
        if (s == null || s.length() == 0) {
            return new ArrayList<>();
        }

        StringBuilder sb = new StringBuilder();
        List<String> res = new ArrayList<>();
        int beginIndex = 0;
        int segmentCount = 0;

        restoreIpAddressesUtil(s, beginIndex, segmentCount, sb, res);

        return res;
    }

    private void restoreIpAddressesUtil(String s, int beginIndex, int segmentCount, StringBuilder sb, List<String> res) {
        if (segmentCount == IP_SEGMENT_COUNT || beginIndex == s.length()) {
            if (segmentCount == IP_SEGMENT_COUNT && beginIndex == s.length()) {
                res.add(sb.toString());
            }
            return;
        }

        int sbLen = sb.length();

        for (int len = 1; len <= MAX_LENGTH; len++) {
            int endIndex = beginIndex + len;

            if (endIndex > s.length()) {
                return;
            }

            String str = s.substring(beginIndex, endIndex);

            if (isValid(str)) {
                // We don't need a dot (.) in the beginning.
                if (sbLen == 0) {
                    sb.append(str);
                } else {
                    sb.append("." + str);
                }
                restoreIpAddressesUtil(s, endIndex, segmentCount + 1, sb, res);
                // Backtracking
                sb.setLength(sbLen);
            }
        }
    }

    private boolean isValid(String str) {
        // 1. Check length.
        if (str == null || str.length() == 0 || str.length() > MAX_LENGTH) {
            return false;
        }

        // 2. Check leading 0.
        if (str.length() > 1 && str.charAt(0) == '0') {
            return false;
        }

        // 3. Check max number.
        int num = Integer.valueOf(str);
        if (num > MAX_INT) {
            return false;
        }

        return true;
    }
}
```
