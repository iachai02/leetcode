# 20. Valid Parenthesis

Given a string s containing just the characters `(`, `)`, `{`, `}`, `[`, `]`, determine if the input string is valid. An input string is valid if:
1. Open brackets must be closed by the same type of brackets
2. Open brackets must be closed in the correct order

- Solution: idea is to use a stack given a map of the valid characters being used. We would pop out the brackets once an open bracket has a closed bracket

```python
def isValid(self, s: str) -> bool:
    Map = {")": "(", "]", "[", "}", "{"}
    stack = []

    # iterate through the string
    for c in s:
        # check if the character is a closing bracket
        if c in Map:
            # if stack is not empty and the top of th estack (last element) is the matching opening bracket for 'c'
            # pop that value out
            if stack and stack[-1] == Map[c]:
                stack.pop()
            else:
                return False
        # if it is an opening bracket, add it to the stack
        else:
            stack.append(c)
        # returns true if the stack is empty
        return not stack
```
- Time: `O(n)`
- Space: `O(n)`

## Example

1. `s = "()[]{}"`
2. Iterate through each letter in string `s`
3. `(` is not in `Map`, so `stack.append('(')`
4. `)` is in `Map`
- stack is not empty and the last element in stack `(` is in `Map[c]`
- pop out `(`, stack is empty
5. Do the same for the other characters
6. return `True` because stack is empty