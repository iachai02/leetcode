# 1. Two Sum

Given an array of integers, return indices of the two numbers such that they add up to a specific target. You may assume that each input would have exactly one solution, and you may not use the same element twice.
- Brute Force: check every combination of two elements and see if they add up to the target
    - Time: `O(n^2)`
- Use hashmap

```python
def twoSum(self, nums: List[int], target: int) -> List[int]:
    # val : idx
    prevMap = {}

    # iterate through the list of nums
    # i: index
    # n: value
    for i, n in enumerate(nums):
        # find the second value that adds up to the target
        diff = target - n

        # checks if that value is in the hashmap
        if diff in prevMap:
            # returns the index of the value and the other value itself
            return [prevMap[diff], i]

        # adds the value with the index to the hashmap
        prevMap[n] = i 
```
Time: `O(n)`
Space: `O(n)`