# 704. Binary Search

Given an array of integers `nums` which is sorted in ascending order, and an integer `target`, write a function to search `target` in `nums`. If `target` exists, then return its index. Otherwise, return `-1`. You must write an algorithm with `O(logn)` runtime complexity.

- Use two pointer and using binary search

```python
def search(self, nums: List[int], target: int) -> int:
    # create a left pointer at 0 and a right pointer at the end of the list
    l, r = 0, len(nums) - 1

    # checks til the right pointer is less than the left pointer
    while l <= r:
        # gets the mid point
        m = l + ((r - l) // 2) # can also use (l + r) // 2

        # checks if the value at the midpoint is larger than the target
        # change the right pointer to one less than the midpoint since it is in lower half of the list
        if nums[m] > target:
            r = m - 1
        
        # checks if the value at the midpoint is smaller than the target
        # change the left pointer to one more than the midpoint since it is in the upper half of the list
        elif nums[m] < target:
            l = m + 1
        else:
            return m
    return -1
```
- Time: `O(logn)` -> because we are constantly finding the mid point which means we are dividing by 2 every time
- Space: `O(1)`

## Example

1. `nums = [-1, 0, 3, 5, 9, 12]`, `target = 9`
2. `l = 0`, `r = 6 - 1 = 5`
3. `l <= r`, `m = (5 + 2) // 2 = 3`
4. `nums[3] = 5 < 9`, `l = 3 + 1 = 4`
5. `l = 4`, `r = 5`, `m = (4 + 5) // 2 = 4`
6. `nums[4] = 9 = 9`
7. return `m = 4`