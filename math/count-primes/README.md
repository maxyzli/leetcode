# Count Primes

## Solution 1

```java
/**
 * Question   : 204. Count Primes
 * Complexity : Time: O(n*log(log(n))) ; Space: O(n)
 * Topics     : Math
 */
class Solution {
    public int countPrimes(int n) {
        if (n <= 1) {
            return 0;
        }

        boolean[] isPrime = new boolean[n];
        Arrays.fill(isPrime, true);
        isPrime[0] = false;
        isPrime[1] = false;

        int count = 0;

        for (int i = 2; i < n; i++) {
            if (isPrime[i]) {
                count++;
                for (int j = i + i; j < n; j += i) {
                    isPrime[j] = false;
                }
            }
        }

        return count;
    }
}
```
