# 150. Evaluate Reverse Polish Notation

You are given an array of strings `tokens` that represents an arithmetic expression in a Reverse Polish Notation. Evaluate the expression. Return an integer that represents the value of the expression.

## Solution

```python

def evalRPN(self, tokens: List[str]) -> int:
    stack = []

    # iterate through the list from left to right
    for n in tokens:
        # if we find the "+", then add the two values from the stack
        if n == "+":
            stack.append(stack.pop() + stack.pop())

        # if we find the "-", then subtract the two values from the stack (first value, then second)
        elif n == "-":
            a, b = stack.pop(), stack.pop()
            stack.append(b - a)

        # if we find the "*", then multiply the two values from the stack
        elif n == "*":
            stack.append(stack.pop() * stack.pop())

        # if we find the "/", then divide the two values from the stack (make sure to convert to int since it will round it down or up to 0)
        elif n == "/":
            a, b = stack.pop(), stack.pop()
            stack.append(int(b / a))

        # add the number to the stack
        else:
            stack.append(int(n))
    # will only have one value in the stack
    return stack[0]

```

- Time: `O(n)`
- Space: `O(n)`

## Example

1. tokens = `["2", "1", "+", "3", "*"]`
2. stack = []
3. n = "2", stack = [2]
4. n = "1", stack = [2, 1]
5. n = "+", stack = [3]
6. n = "3", stack = [3, 3]
7. n = "\*", stack = [9]
8. return `9`
