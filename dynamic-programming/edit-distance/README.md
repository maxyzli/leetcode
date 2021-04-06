# Edit Distance

## Solution 1

```java
import java.util.*;

/**
 * Question   : 72. Edit Distance
 * Complexity : Time: O(m*n) ; Space: O(m*n)
 * Topics     : DP
 */
class Solution {
    public int minDistance(String A, String B) {
        if (A == null && B == null) {
            return 0;
        }
        if (A.length() == 0 && B.length() == 0) {
            return 0;
        }

        // We want to change A to B.
        int[][] distance = new int[B.length() + 1][A.length() + 1];

        //    " h o r s e (A)
        // "
        // r
        // o
        // s
        //(B)

        // Transform A to empty B always performs "deletion".
        for (int j = 1; j <= A.length(); j++) {
            distance[0][j] = distance[0][j - 1] + 1;
        }

        //    " h o r s e (A)
        // "  0 1 2 3 4 5
        // r
        // o
        // s
        //(B)

        // Transform empty A to B always performs "insertion".
        for (int i = 1; i <= B.length(); i++) {
            distance[i][0] = distance[i - 1][0] + 1;
        }

        //    " h o r s e (A)
        // "  0 1 2 3 4 5
        // r  1
        // o  2
        // s  3
        //(B)

        for (int i = 1; i <= B.length(); i++) {
            for (int j = 1; j <= A.length(); j++) {
                char charA = A.charAt(j - 1);
                char charB = B.charAt(i - 1);
                // If 2 characters are the same,
                // the edit distance is the same as without them.
                if (charA == charB) {
                    distance[i][j] = distance[i - 1][j - 1];
                    continue;
                }

                // If 2 characters are not the same,
                // we can perform "insertion", "deletion" or "replacement".
                int insert = distance[i][j - 1];
                int delete = distance[i - 1][j];
                int replace = distance[i - 1][j - 1];

                distance[i][j] = 1 + Math.min(insert, Math.min(delete, replace));
            }
        }

        return distance[B.length()][A.length()];
    }
}
```
