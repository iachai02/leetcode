# 84. Largest Rectangle in Histogram

Given an array of integers `heights` representing the histogram's bar height where the width of each bar is `1`, return the area of the largest rectangle in the histogram.

## Solution

```python
def largestRectangleArea(self, heights: List[int]) -> int:
    stack = [] # stores [index, height]
    max_area = 0

    # iterate through the heights getting the index and the height
    for i, h in enumerate(heights):
        start = i

        # if the current bar is shorter than the height of the bar at the top of the stack, the height of the popped bar can no longer further extend to the right
        while stack and h < stack[-1][1]:
            index, height = stack.pop()
            max_area = max(area, height * (i - index))
            start = index
        stack.append((start, h))

    # goes through the stack with the remaining bars that go to the end of the histogram
    for i, h in stack:
        max_area = max(max_area, h * (len(heights) - i))
    return max_area
```

- Time: `O(n)`
- Space: `O(n)`

## Example

1. heights = [7, 1, 7, 2, 2, 4]
2. start = 0, stack = [[0, 7]]
3. 1 < 7, index = 0, height = 7, max_area = 0 or 7 = 7, start = 0, stack = [[0, 1]]
4. 7 > 1, stack = [[0, 1], [2, 7]]
5. 2 < 7, index = 2, height = 7, max_area = 7 or 7 = 7, start = 2, stack = [[0, 1], [2, 2]]
6. 2 < 2, stack = [[0, 1], [2, 2], [2, 2]]
7. 4 > 2, stack = [[0, 1], [2, 2], [4, 2], [5, 4]]
8. go through the stack
9. max_area = 7 or 1 \* (6 - 0) = 6 = 7
10. max_area = 7 or 2 \* (6 - 2) = 8 = 8
11. max_area = 8 or 2 \* (6 - 4) = 4 = 8
12. max_area = 8 or 4 \* (6 - 5) = 4 = 8
13. return max_area = 8
