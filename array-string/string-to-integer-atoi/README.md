# String to Integer (atoi)

## Solution 1

Use Long

```java
/**
 * Question   : 8. String to Integer (atoi)
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : string
 */
class Solution {
    public int myAtoi(String s) {
        if (s == null) {
            return 0;
        }

        // 1. Read in and ignore any leading whitespace.
        s = s.strip();
        if (s.length() == 0) {
            return 0;
        }

        // 2. Check if the next character (if not already at the end of the string) is '-' or '+'.
        int i = 0;
        int sign = 1;
        if (s.charAt(i) == '+' || s.charAt(i) == '-') {
            if (s.charAt(i) == '-') {
                sign = -1;
            }
            i++;
        }

        // 3. Check if the first character is a digit.
        if (i >= s.length() || !Character.isDigit(s.charAt(i))) {
            return 0;
        }

        // 4. Read in next the characters until the next non-digit character or the end of the input is reached.
        int j = i;
        while (j < s.length() && Character.isDigit(s.charAt(j))) {
            j++;
        }

        // 5. Convert these digits into an integer
        long number = 0;
        while (i < j) {
            number = number * 10 + (s.charAt(i) - '0');
            i++;
            // 6. Clamp the integer
            if (sign > 0 && number > Integer.MAX_VALUE) {
                return Integer.MAX_VALUE;
            }
            if (sign < 0 && -number < Integer.MIN_VALUE) {
                return Integer.MIN_VALUE;
            }
        }

        // 8. Return the integer as the final result.
        return sign * (int)number;
    }
}
```

## Solution 2

```java
/**
 * Question   : 8. String to Integer (atoi)
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : string
 */
class Solution {
    public int myAtoi(String s) {
        if (s == null) {
            return 0;
        }

        // 1. Read in and ignore any leading whitespace.
        s = s.strip();
        if (s.length() == 0) {
            return 0;
        }

        // 2. Check if the next character (if not already at the end of the string) is '-' or '+'.
        int i = 0;
        int sign = 1;
        if (s.charAt(i) == '+' || s.charAt(i) == '-') {
            if (s.charAt(i) == '-') {
                sign = -1;
            }
            i++;
        }

        // 3. Check if the first character is a digit.
        if (i >= s.length() || !Character.isDigit(s.charAt(i))) {
            return 0;
        }

        // 4. Read in next the characters until the next non-digit character or the end of the input is reached.
        int j = i;
        while (j < s.length() && Character.isDigit(s.charAt(j))) {
            j++;
        }

        // 5. Convert these digits into an integer
        int number = 0;
        while (i < j) {
            // 6. Clamp the integer
            // -2147483648 ~ 2147483647
            if (
                    number > Integer.MAX_VALUE / 10 ||
                    (number == (Integer.MAX_VALUE / 10) && s.charAt(i) - '0' > 7)
            ) {
                if (sign > 0) {
                    return Integer.MAX_VALUE;
                } else {
                    return Integer.MIN_VALUE;
                }
            }
            number = number * 10 + (s.charAt(i) - '0');
            i++;
        }

        // 8. Return the integer as the final result.
        return sign * number;
    }
}
```
