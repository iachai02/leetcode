# 22. Generate Parentheses

Given `n` pairs of parentheses, write a function to generate all combinations of well-formed parentheses

## Solution

```python
def generateParenthesis(self, n: int) -> List[str]:
    ans = []
    stack = []

    # openN: keeps track of number of open brackets
    # closedN: keeps track of number of closed brackets
    def backtrack(openN, closedN):
        # base case: if the number of open and closed brackets equal n, then add that answer to the array
        if openN == closedN == n:
            ans.append("".join(stack))
            return

        # case 1: if the amount of open brackets is less than n
        if openN < n:
            # add the open bracket to the stack
            stack.append("(")

            # recursively call the function again, but with the number of open brackets increased by one
            backtrack(openN + 1, closedN)

            # need to pop it from the stack to its original state
            stack.pop()

        # case 2: if the amount of closed brackets is less than the amount of open brackets
        if closedN < openN:
            # add the closed bracket to the stack
            stack.append(")")

            # recursively call the function again, but with the number of closed brackets increased by one
            backtrack(openN, closedN + 1)

            # need to pop it from the stack to its original state
            stack.pop()

    # start when there are no open or closed brackets
    backtrack(0, 0)
    return ans
```

- Time: `O(4^n/(n)^1/2)`
- Space: `O(n)`

## Example

1. n = 2, ans = [], stack = [], call backtrack(0, 0)
2. a. openN < n (0 < 2): stack = [(], backtrack(1, 0), stack = []
   a. openN < n (1 < 2): stack = [((], backtrack(2, 0), stack = [(]
   - closedN < openN (0 < 2): stack = [(()], backtrack(2, 1), stack = [((]
   - closedN < openN (1 < 2): stack = [(())], backtrack(2, 2), stack = [(()]
   - openN = closedN = n = 2, res = [(())]
     b. closedN < openN (0 < 1): stack = [()], backtrack(1, 1), stack = [(]
   - openN < n (1 < 2): stack = [()(], backtrack(2, 1), stack = [()]
   - closedN < openN (1 < 2): stack = [()()], backtrack(2, 2), stack = [()(]
   - openN = closedN = n = 2, res = [(()), ()()]
3. return res = [(()), ()()]
