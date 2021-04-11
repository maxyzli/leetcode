# Reverse Linked List

## Solution 1

Iteration

```java
/**
 * Question   : 206. Reverse Linked List
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Linked List
 */
var reverseList = function(head) {
    // Create pointers
    let prev = null;
    let curr = head;
    let next = null;

    // While
    while (curr != null) {
        next = curr.next;
        curr.next = prev;
        // move the pointers
        prev = curr;
        curr = next;
    }


    // Return the result
    return prev;
};
```

## Solution 2

Recursion

```java
/**
 * Question   : 206. Reverse Linked List
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Linked List
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode newHead = reverseList(head.next);
        head.next.next = head;
        head.next = null;
        return newHead;
    }
}
```
