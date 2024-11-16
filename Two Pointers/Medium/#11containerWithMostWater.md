# 11. Container With Most Water

You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `ith` line are `(i, 0)` and `(i, height[i])`. Find two lines that together with the x-axis form a container, such that the container contains the most water. Return the maximum amount of water a container can store. Notice that you may not slant the container.

## Solution

```python
def maxArea(self, height: List[int]) -> int:
    l, r = 0, len(height) - 1
    max_area = 0

    while l < r:
        area = (r-l) * min(height[l], height[r])
        max_area = max(max_area, area)
        if height[l] < height[r]:
            l += 1
        else:
            r -=1
    return max_area
```

- Time: `O(n)`
- Space: `O(1)`

## Example

1. input = `height = [1, 8, 6, 2, 5, 4, 8, 3, 7]`
2. l = 0, r = 8, max_area = 0
3. area = 8 \* 1 = 8
4. max_area = 8 or 0 = 8
5. l += 1 = 1, r = 8
6. area = 7 \* 7 = 49
7. max_area = 8 or 49 = 49
8. l = 1, r -= 1 = 7
9. area = 6 \* 3 = 18
10. max_area = 49 or 18 = 49
11. l = 1, r -= 1 = 6
12. area = 5 \* 8 = 40
13. max_area = 49 or 40 = 49
14. go through the entire loop
15. return 49
