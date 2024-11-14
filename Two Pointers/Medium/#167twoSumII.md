# 167. Two Sum II - Input Array is Sorted

Given a 1-indexed array of integers `numbers` that is already sorted in non-decreasing order, find two numbers such that they add up to a specific `target` number. Let these two numbers be `numbers[index1]` and `numbers[index2]` where 1 <= index1 < index2 <= numbers.length. Return the indices of the two numbers, `index1` and `index2`, added by one as an integer array `[index1, index2]` of length 2. The tests are generated such that there is exactly one solution. You may not use the same element twice. Your solution must use only constant extra space.

## Solution

```python
def twoSum(self, numbers: List[int], target: int) -> List[int]:
    l, r = 0, len(numbers) - 1
    while l < r:
        curSum = numbers[l] + numbers[r]
        if curSum > target:
            r -= 1
        elif curSum < target:
            l += 1
        else:
            return [l+1, r+1]
```

- Time: O(n)
- Space: O(1)

## Example

1. `input`: `[2, 3, 4]`, `target` = 6
2. l = 0, r = 2
3. `curSum` = 2 + 4 = 6
4. `curSum` = `target` = 6
5. return [0 + 1, 2 + 1] = [1, 3]
