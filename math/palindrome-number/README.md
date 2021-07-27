# Palindrome Number

## Solution 1

```java
class Solution {
  public boolean isPalindrome(int x) {
    if (x == 0) {
      return true;
    }
    if (x < 0) {
      return false;
    }

    int numDigit = (int) Math.log10(x) + 1;
    int mask = (int) Math.pow(10, numDigit - 1);

    for (int i = 0; i < numDigit / 2; i++) {
      if ((x / mask) != x % 10) {
        return false;
      }

      x %= mask;
      x /= 10;

      // Remove 2 0's from the mask since we just lost 2 digits
      mask /= 100;
    }

    return true;
  }
}
```
