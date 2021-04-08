# Implement Queue using Stacks

## Solution 1

Two Stack

```java
import java.util.*;

class MyQueue {
    Stack<Integer> stack1;
    Stack<Integer> stack2;

    public MyQueue() {
        stack1 = new Stack<>();
        stack2 = new Stack<>();
    }

    public void push(int x) {
        stack1.push(x);
    }

    public int pop() {
        if (stack2.isEmpty()) {
            while (!stack1.isEmpty()) {
                stack2.push(stack1.pop());
            }
        }
        return stack2.pop();
    }

    public int peek() {
        if (stack2.isEmpty()) {
            while (!stack1.isEmpty()) {
                stack2.push(stack1.pop());
            }
        }
        return stack2.peek();
    }

    public boolean empty() {
        return stack1.isEmpty() && stack2.isEmpty();
    }
}
```

## Solution 2

One Stack

```java
import java.util.*;

class MyQueue {
    Stack<Integer> stack;

    public MyQueue() {
        stack = new Stack<>();
    }

    public void push(int x) {
        if (stack.isEmpty()) {
            stack.push(x);
            return;
        }
        int temp = stack.pop();
        push(x);
        stack.push(temp);
    }

    public int pop() {
        return stack.pop();
    }

    public int peek() {
        return stack.peek();
    }

    public boolean empty() {
        return stack.isEmpty();
    }
}
```
