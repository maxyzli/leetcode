# Palindrome Number

# Solution 1

Conver to string

```java
/**
 * Question   : 9. Palindrome Number
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : String
 * Date       : 2021/04/06
 */
class Solution {
    public boolean isPalindrome(int x) {
        if (x == 0) {
            return true;
        }
        if (x < 0) {
            return false;
        }

        String str = x + "";

        int low = 0;
        int high = str.length() - 1;

        while (low < high) {
            if (str.charAt(low) != str.charAt(high)) {
                return false;
            }
            low++;
            high--;
        }

        return true;
    }
}
```

# Solution 2

Math

```java
/**
 * Question   : 9. Palindrome Number
 * Complexity : Time: O(1) ; Space: O(1)
 * Topics     : Math
 */
class Solution {
    public boolean isPalindrome(int x) {
        if (x == 0) {
            return true;
        }
        if (x < 0) {
            return false;
        }

        int temp = x;
        int y = 0;

        while (temp != 0) {
            y = (y * 10) + (temp % 10);
            temp /= 10;
        }

        return x == y;
    }
}
```
