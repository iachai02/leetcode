# 42. Trapping Rain Water

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

## Solution 1 (get the max height on left and right using arrays)

```python
def trap(self, height: List[int]):
    # This handles the edge case
    n = len(height)
    if n == 0:
        return 0

    # Stores the tallest bar to the left of or at index i
    leftMax = [0] * n

    # Stores the tallest bar to the right of or at index i
    rightMax = [0] * n

    # Start at the first index
    # At each index, calculate the tallest bar to the left
    leftMax[0] = height[0]
    for i in range(1, n):
        leftMax[i] = max(leftMax[i-1], height[i])

    # Start at the last index
    # At each index, calculate the tallest bar to the right
    rightMax[n - 1] = height[n - 1]
    for i in range(n - 2, -1, -1):
        rightMax[i] = max(rightMax[i+1], height[i])

    # stores the amount of water
    res = 0

    # get the shorter of the two boundaries at index i and subtract that from the height and add that to the amount of water
    for i in range(n):
        res += min(leftMax[i], rightMax[i]) - height[i]
    return res
```

- Time: `O(n)`
- Space: `O(n)`

## Solution 2 (no extra space needed)

```python
def trap(self, height: List[int]):
    # edge case in case there is nothing in the height array
    if not height: return 0

    # get the left and right pointer of the entire array
    l, r = 0, len(height)-1

    # get the initial maxes of the left and right pointer
    leftMax, rightMax = height[l], height[r]

    # total amount of water
    res = 0
    while l < r:
        # whatever max is smaller, move that pointer over
        if leftMax < rightMax:
            # move the left pointer
            l += 1

            # get the left max at and from height at the left pointer
            leftMax = max(leftMax, height[l])

            # add the left max with the height if height is less than the left max
            res += leftMax - height[l]
        else:
            # move the right pointer
            r -= 1

            # get the right max at and from height at the right pointer
            rightMax = max(rightMax, height[r])

            # add the right max with the height if height is less than the right max
            res += rightMax - height[r]
    return res
```

- Time: `O(n)`
- Space: `O(1)`

## Example

1. height = `[4, 2, 0, 3, 2, 5]`
2. l = 0, r = 5, leftMax = 4, rightMax = 5
3. 4 < 5, so l += 1 = 1, leftMax = 4, res += 4 - 2 = 2
4. 4 < 5, so l += 1 = 2, leftMax = 4, res += 4 - 0 = 4
5. 4 < 5, so l += 1 = 3, leftMax = 4, res += 4 - 3 = 1
6. 4 < 5, so l += 1 = 4, leftMax = 4, res += 4 - 2 = 2
7. 4 < 5, so l += 1 = 5 = r = 5
8. return res = 2 + 4 + 1 + 2 = 9
