# Roman to Integer

## Solution 1

```java
/**
 * Question   : 13. Roman to Integer
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : String
 */
class Solution {
    public int romanToInt(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }

        int n = s.length();
        int sum = 0;
        int pre = getValue(s.charAt(0));

        for (int i = 1; i < n; i++) {
            int curr = getValue(s.charAt(i));
            if (pre < curr) {
                sum -= pre;
            } else {
                sum += pre;
            }
            pre = curr;
        }
        
        sum += getValue(s.charAt(n - 1));

        return sum;
    }

    private int getValue(char ch) {
        switch (ch) {
            case 'I': return 1;
            case 'V': return 5;
            case 'X': return 10;
            case 'L': return 50;
            case 'C': return 100;
            case 'D': return 500;
            case 'M': return 1000;
            default: return 0;
        }
    }
}
```
