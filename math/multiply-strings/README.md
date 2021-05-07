# Multiply Strings

## Solution 1

```java
/**
 * Question   : 43. Multiply Strings
 * Complexity : Time: O(m*(m+n)) ; Space: O(m+n)
 * Topics     : Math
 */
public class Solution {
    public String multiply(String num1, String num2) {
        if (num1.equals("0") || num2.equals("0")) {
            return "0";
        }

        int m = num1.length();
        int n = num2.length();

        String ans = "0";
        StringBuilder temp = new StringBuilder();

        for (int j = n - 1; j >= 0; j--) {
            // Append Zero.
            for (int k = 0; k < n - 1 - j; k++) {
                temp.append("0");
            }

            int b = (num2.charAt(j) - '0');
            int carry = 0;

            for (int i = m - 1; i >= 0; i--) {
                int a = (num1.charAt(i) - '0');
                int product = a * b + carry;
                temp.append(product % 10);
                carry = product / 10;
            }

            if (carry > 0) {
                temp.append(carry);
            }
            
            // Add Two Number String.
            ans = addStrings(ans, temp.reverse().toString());
            
            // Reset. 
            temp.setLength(0);
        }

        return ans;
    }

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

## Solution 2

```java
/**
 * Question   : 43. Multiply Strings
 * Complexity : Time: O(m*n) ; Space: O(m*n)
 * Topics     : Math
 */
public class Solution {
    public String multiply(String num1, String num2) {
        if (num1.equals("0") || num2.equals("0")) {
            return "0";
        }

        int m = num1.length();
        int n = num2.length();

        int[] res = new int[m + n];

        // Example:
        //
        // i    : 0 1 2 3
        // num1 : 3 2 4 9
        //
        // j    :   0 1 2
        // num2 :   5 6 4
        //
        // k    : 0 1 2 3 4 5 6
        // res  : 0 0 0 0 0 0 0
        //            1 2 9 9 6
        //          1 9 4 9 4 0
        //        1 6 2 4 5 0 0

        for (int j = n - 1; j >= 0; j--) {
            int b = (num2.charAt(j) - '0');
            int carry = 0;

            for (int i = m - 1; i >= 0; i--) {
                int a = (num1.charAt(i) - '0');
                int sum = res[i + j + 1] + a * b + carry;
                res[i + j + 1] = sum % 10;
                carry = sum / 10;
            }

            if (carry > 0) {
                res[j] = carry;
            }
        }

        // Skip Leading Zeros.
        int beginIndex = 0;
        while (res[beginIndex] == 0) {
            beginIndex++;
        }

        StringBuilder sb = new StringBuilder();
        for (int i = beginIndex; i < res.length; i++) {
            sb.append(res[i]);
        }

        return sb.toString();
    }
}
```
