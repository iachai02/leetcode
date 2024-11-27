# 739. Daily Temperatures

Given an array of integers `temperatures` represents the daily temperatures, return an array `answer` such that `answer[i]` is the number of days you have to wait after the `ith` day to get a warmer temperature. If there is no future day for which it is possible, keep `answer[i] == 0` instead.

## Solution

```python
def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
    res = [0] * len(temperatures)
    stack = [] # hold values [temperature, index]

    # iterate through the temperatures array using the index and the temperature
    for i, t in enumerate(temperatures):
        # checks if stack is not empty
        # compares the temperature with the temperature at the top of the stack
        while stack and t > stack[-1][0]:
            # gets the top of the stack's temperature and index
            stackT, standInd = stack.pop()

            # adds the value of how many days until a warmer day to the res array
            res[stackInd] = i - stackInd

        # adds the temperature and the index to the array if the current temperature t is not greater than the top of the stack
        stack.append([t, i])
    return res
```

- Time: `O(n)`
- Space: `O(n)`

## Example

1. temperatures = `[73, 74, 75, 71, 69, 72, 76, 73]`
2. res = `[0, 0, 0, 0, 0, 0, 0, 0]`, stack = []
3. stack = [[73, 0]]
4. 74 > 73, so stack = [], stackInd = 0, res[0] = 1 - 0 = 1, res = [1, 0, 0, 0, 0, 0, 0, 0]
5. stack = [[74, 1]]
6. 75 > 74, so stack = [], stackInd = 1, res[1] = 2 - 1 = 1, res = [1, 1, 0, 0, 0, 0, 0, 0]
7. stack = [[75, 2]]
8. 71 < 75, stack = [[75, 2], [71, 3]]
9. 69 < 71, stack = [[75, 2], [71, 3], [69, 4]]
10. 72 > 69, so stack = [[75, 2], [71, 3]], stackInd = 4, res[4] = 5 - 4 = 1, res = [1, 1, 0, 0, 1, 0, 0, 0]
11. 72 > 71, so stack = [[75, 2]], stackInd = 3, res[3] = 5 - 3 = 2, res = [1, 1, 0, 2, 1, 0, 0, 0]
12. 72 < 75, so stack = [[75, 2], [72, 5]]
13. 76 > 72, so stack = [[75, 2]], stackInd = 5, res[5] = 6 - 5 = 1, res = [1, 1, 0, 2, 1, 1, 0, 0]
14. 76 > 75, so stack = [], stackInd = 2, res[2] = 6 - 2 = 4, res = [1, 1, 4, 2, 1, 1, 0, 0]
15. stack = [[76, 6]]
16. 73 < 76, so stack = [[76, 6], [73, 7]]
17. return res = [1, 1, 4, 2, 1, 1, 0, 0]
