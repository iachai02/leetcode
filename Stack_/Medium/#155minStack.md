# 155. Min Stack

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time. Implement the `minStack` class: - `MinStack()` initializes the stack object - `void push(int val)` pushes the element `val` onto the stack - `void pop()` removes the element on the top of the stack. - `int top()` gets the top element of the stack - `int getMin()` retrieves the minimum element in the stack.

You must implement a solution with `O(1)` time complexity for each function.

## Solution

```python
class MinStack:
    def __init__(self):
        # keeps track of the actual stack
        self.stack = []

        # keeps track of the minimum values corresponding to the elements in the stack
        self.minStack = []

    def push(self, val: int) -> None:
        # push the value to the stack
        self.stack.append(val)

        # gets the minimum value when adding value to the stack (val could be the minimum or the minStack[-1] could still be the minimum)
        val = min(val, self.minStack[-1] if self.minStack else val)

        # add whatever was the minimum to the minStack
        self.minStack.append(val)

    def pop(self) -> None:
        # pop the top of the stack
        self.stack.pop()

        # pop the minimum value corresponding to the value popped which is why we pop it off as well
        self.minStack.pop()

    def top(self) -> int:
        # gets the top of the stack
        return self.stack[-1]

    def getMin(self) -> int:
        # the top of the min value stack is the min value
        return self.minStack[-1]
```

- Time: `O(1)`
- Space: `O(n)`
