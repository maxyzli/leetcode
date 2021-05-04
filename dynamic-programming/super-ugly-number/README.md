# Super Ugly Number

## Solution 1

Brute Force

```java
/**
 * Question   : 313. Super Ugly Number
 * Complexity : Time: O(mn) ; Space: O(1)
 * Topics     : Brute Force
 */
public class Solution {
    public int nthSuperUglyNumber(int n, int[] primes) {
        if (n < 0 || primes.length == 0) {
            return 0;
        }
        if (n == 1) {
            return 1;
        }

        int count = 1;
        int num = 1;

        while (count < n) {
            num++;
            if (isUgly(num, primes)) {
                count++;
            }
        }

        return num;
    }

    private boolean isUgly(int num, int[] primes) {
        int curr = num;
        while (true) {
            boolean divisible = false;
            for (int i = 0; i < primes.length; i++) {
                if (curr % primes[i] == 0) {
                    curr /= primes[i];
                    divisible = true;
                    break;
                }
            }
            if (!divisible) {
                return false;
            }
            if (curr == 1) {
                return true;
            }
        }
    }
}
```

## Solution 2

DP

```java
/**
 * Question   : 313. Super Ugly Number
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : DP
 */
class Solution {
    public int nthSuperUglyNumber(int n, int[] primes) {
        int dp[] = new int[n];
        dp[0] = 1;

        int len = primes.length;
        int index[] = new int[len];

        for (int i = 1; i < n; i++) {
            int min = Integer.MAX_VALUE;
            for (int j = 0; j < len; j++) {
                min = Math.min(min, primes[j] * dp[index[j]]);
            }
            dp[i] = min;

            for (int j = 0; j < len; j++) {
                if (min == primes[j] * dp[index[j]]) {
                    index[j]++;
                }
            }
        }

        return dp[n - 1];
    }
}
```
