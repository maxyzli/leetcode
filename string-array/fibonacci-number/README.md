# Fibonacci Number

## Solution 1

Native Approach

```java
class Solution {
    public int fib(int n) {
       if (n == 0) {
            return 0;
        }
        if (n == 1) {
            return 1;
        }
        return fib(n - 1) + fib(n - 2);
    }
}
```

## Solution 2

DP

```java
class Solution {
    public int fib(int n) {
        int SIZE = 31;
        int[] m = new int[SIZE];
        m[0] = 0;
        m[1] = 1;
        return fibUtil(n, m);
    }

    static private int fibUtil(int n, int[] m) {
        if (n == 0 || m[n] != 0) {
            return m[n];
        }

        int res = fibUtil(n - 1, m) + fibUtil(n - 2, m);
        m[n] = res;

        return res;
    }
}
```

## Solution 3

Constant DP

```java
class Solution {
    public int fib(int n) {
        if (n == 0) {
            return 0;
        }
        if (n == 1) {
            return 1;
        }

        int prev = 0;
        int curr = 1;

        for (int i = 2; i <= n; i++) {
            int next = prev + curr;
            prev = curr;
            curr = next;
        }

        return curr;
    }
}
```
