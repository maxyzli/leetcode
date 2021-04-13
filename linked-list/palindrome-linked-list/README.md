# Palindrome Linked List

## Solution 1

Stack

```java
/**
 * Question   : 234. Palindrome Linked List
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Linked List
 */
class Solution {
    public boolean isPalindrome(ListNode head) {
        Stack<ListNode> stack = new Stack<>();

        ListNode p = head;
        while (p != null) {
            stack.add(p);
            p = p.next;
        }

        p = head;
        while (p != null) {
            if (p.val != stack.pop().val) {
                return false;
            }
            p = p.next;
        }

        return true;
    }
}
```

## Solution 2

Reverse

```java
/**
 * Question   : Palindrome Linked List
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Linked List
 */
public class Solution {
    public boolean isPalindrome(ListNode head) {
        if (head == null || head.next == null) {
            return true;
        }

        ListNode prev = null;
        ListNode slow = head;
        ListNode fast = head;

        while (fast != null && fast.next != null) {
            prev = slow;
            slow = slow.next;
            fast = fast.next.next;
        }
        prev.next = null;

        ListNode p1 = reverse(head);
        ListNode p2;
        // Even
        if (fast == null) {
            p2 = slow;
        } else {
            p2 = slow.next;
        }

        while (p1 != null || p2 != null) {
            if (p1 == null || p2 == null) {
                return false;
            }
            if (p1.val != p2.val) {
                return false;
            }
            p1 = p1.next;
            p2 = p2.next;
        }

        return true;
    }

    private ListNode reverse(ListNode head) {
        if (head.next == null) {
            return head;
        }
        ListNode newHead = reverse(head.next);
        head.next.next = head;
        head.next = null;
        return newHead;
    }
}
```

## Solution 3

Recursion

```java
/**
 * Question   : 234. Palindrome Linked List
 * Complexity : Time: O(n) ; Space: O(1)
 * Topics     : Linked List
 */
class Solution {
    ListNode left;

    public boolean isPalindrome(ListNode head) {
        if (head == null) {
            return true;
        }
        left = head;
        return isPalindromeUtil(head);
    }

    public boolean isPalindromeUtil(ListNode head) {
        if (head == null) {
            return true;
        }

        if (!isPalindromeUtil(head.next)) {
            return false;
        };

        if (left.val != head.val) {
            return false;
        }
        left = left.next;

        return true;
    }
}
```
