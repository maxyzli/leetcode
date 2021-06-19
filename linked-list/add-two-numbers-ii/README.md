# Add Two Numbers II

## Solution 1

Reverse

```java
/**
 * Question   : 445. Add Two Numbers II
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Linked List
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode list1 = reverse(l1);
        ListNode list2 = reverse(l2);

        ListNode dummy = new ListNode(0);
        ListNode p = dummy;

        int carry = 0;
        while (list1 != null || list2 != null) {
            int sum = carry;

            if (list1 != null) {
                sum += list1.val;
                list1 = list1.next;
            }
            if (list2 != null) {
                sum += list2.val;
                list2 = list2.next;
            }

            p.next = new ListNode(sum % 10);
            p = p.next;

            carry = sum / 10;
        }

        if (carry > 0) {
            p.next = new ListNode(carry);
            p = p.next;
        }

        return reverse(dummy.next);
    }

    private ListNode reverse(ListNode node) {
        if (node == null || node.next == null) {
            return node;
        }
        ListNode head = reverse(node.next);
        node.next.next = node;
        node.next = null;
        return head;
    }
}
```

## Solution 2

Stack

```java
/**
 * Question   : 2. Add Two Numbers
 * Complexity : Time: O(n) ; Space: O(n)
 * Topics     : Linked List
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        Stack<Integer> s1 = new Stack<>();
        Stack<Integer> s2 = new Stack<>();

        while (l1 != null) {
            s1.add(l1.val);
            l1 = l1.next;
        }
        while (l2 != null) {
            s2.add(l2.val);
            l2 = l2.next;
        }

        ListNode head = null;
        int carry = 0;
        while (!s1.isEmpty() || !s2.isEmpty()) {
            int sum = carry;
            if (!s1.isEmpty()) {
                sum += s1.pop();
            }
            if (!s2.isEmpty()) {
                sum += s2.pop();
            }

            carry = sum / 10;
            ListNode newNode = new ListNode(sum % 10);

            if (head != null) {
                newNode.next = head;
            }
            head = newNode;
        }
        
        if (carry > 0) {
            ListNode newNode = new ListNode(carry);
            newNode.next = head;
            head = newNode;
        }

        return head;
    }
}
```
