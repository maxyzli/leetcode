# Print Immutable Linked List in Reverse

## Solution 1

```java
/**
 * Question   : 1265. Print Immutable Linked List in Reverse
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Linked List
 */
class Solution {
    public void printLinkedListInReverse(ImmutableListNode head) {
        if (head == null) {
            return;
        }
        printLinkedListInReverse(head.getNext());
        head.printValue();
    }
}
```
