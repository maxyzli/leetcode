# Min Stack

## Solution 1

Two Stack

```java
/**
 * Question   : 155. Min Stack
 * Topics     : Array
 */
class MinStack {
    Stack<Integer> stack;
    Stack<Integer> min;

    public MinStack() {
        stack = new Stack<>();
        min = new Stack<>();
    }

    public void push(int val) {
        stack.add(val);
        if (min.isEmpty()) {
            min.add(val);
        } else {
            min.add(Math.min(min.peek(), val));
        }
    }

    public void pop() {
        stack.pop();
        min.pop();
    }

    public int top() {
        return stack.peek();
    }

    public int getMin() {
        return min.peek();
    }
}
```

## Solution 2

One Stack

```java
/**
 * Question   : 155. Min Stack
 * Topics     : Array
 */
class MinStack {
    private class Node {
        int val;
        int min;
        public Node(int val, int min) {
            this.val = val;
            this.min = min;
        }
    }

    Stack<Node> stack;

    public MinStack() {
        stack = new Stack<>();
    }

    public void push(int val) {
        if (stack.isEmpty()) {
            stack.add(new Node(val, val));
        } else {
            Node temp = stack.peek();
            int min = Math.min(temp.min, val);
            stack.add(new Node(val, min));
        }
    }

    public void pop() {
        stack.pop();
    }

    public int top() {
        return stack.peek().val;
    }

    public int getMin() {
        return stack.peek().min;
    }
}
```
