# Lemonade Change

## Solution 1

HashMap

```java
/**
 * Question   : 860. Lemonade Change
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public boolean lemonadeChange(int[] bills) {
        HashMap<Integer, Integer> changes = new HashMap<>();
        changes.put(5, 0);
        changes.put(10, 0);
        changes.put(20, 0);

        for (int i = 0; i < bills.length; i++) {
            if (bills[i] == 5) {
                changes.put(5, changes.get(5) + 1);
            } else if (bills[i] == 10) {
               if (changes.get(5) >= 1) {
                   changes.put(5, changes.get(5) - 1);
               } else {
                   return false;
               }
               changes.put(10, changes.get(10) + 1);
            } else if (bills[i] == 20) {
                if (changes.get(10) >= 1 && changes.get(5) >= 1) {
                    changes.put(5, changes.get(5) - 1);
                    changes.put(10, changes.get(10) - 1);
                } else if (changes.get(5) >= 3) {
                    changes.put(5, changes.get(5) - 3);
                } else {
                    return false;
                }
                changes.put(20, changes.get(20) + 1);
            }
        }

        return true;
    }
}
```

## Solution 2

Two Variables

```java
/**
 * Question   : 860. Lemonade Change
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Array
 */
class Solution {
    public boolean lemonadeChange(int[] bills) {
        int fiveCount = 0;
        int tenCount = 0;

        for (int i = 0; i < bills.length; i++) {
            if (bills[i] == 5) {
                fiveCount++;
            } else if (bills[i] == 10) {
               if (fiveCount >= 1) {
                   fiveCount--;
               } else {
                   return false;
               }
               tenCount++;
            } else if (bills[i] == 20) {
                if (tenCount >= 1 && fiveCount >= 1) {
                    tenCount--;
                    fiveCount--;
                } else if (fiveCount >= 3) {
                    fiveCount -= 3;
                } else {
                    return false;
                }
            }
        }

        return true;
    }
}
```
