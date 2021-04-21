# Pow(x, n)

## Solution 1

```java
/**
 * Question   : 50. Pow(x, n)
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Math, Divide and Conquer
 */
class Solution {
    public double myPow(double x, int n) {
        if (n == 0) {
            return 1;
        }
        if (n < 0) {
            return 1 / myPow(x, -n);
        }

        return x * myPow(x, n - 1);
    }
}
```

## Solution 2

```java
/**
 * Question   : 50. Pow(x, n)
 * Complexity : Time: O(log(n)) ; Space: O(log(n))
 * Topics     : Math, Divide and Conquer
 */
class Solution {
    public double myPow(double x, int n) {
        if (n == 0) {
            return 1;
        }

        if (n < 0) {
            if (n % 2 == 0) {
                return 1 / myPow(x * x, -(n / 2));
            } else {
                return 1 / (x * myPow(x * x, -(n / 2)));
            }
        }

        if (n % 2 == 0) {
            return myPow(x * x, n / 2);
        } else {
            return x * myPow(x * x, n / 2);
        }
    }
}
```
