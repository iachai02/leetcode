# 128. Longest Consecutive Sequence

Given an unsorted array of integers `nums`, return the length of the longest consecutive elements sequence. You must write an algorithm that runs in O(n) time.

## Brute Force Solution

```python
def longestConsecutive(self, nums: List[int]) -> int:
    res = 0
    store = set(nums)

    # iterates through the nums array
    for num in nums:
        # keeps track of the streak and also the current num
        streak, curr = 0, num
        while curr in store:
            streak += 1
            curr += 1
        res = max(res, streak)
    return res
```

- Time: `O(n^2)`
- Space: `O(n)`

## Sorting Solution

```python
def longestConsecutive(self, nums: List[int]) -> int:
    # check if the list is empty
    if not nums:
        return 0
    res = 0
    nums.sort()

    # gets the current num and the streak of the sequence
    curr, streak = nums[0], 0
    i = 0
    while i < len(nums):
        # if the current number is different from nums[i]
        if curr != nums[i]:
            curr = nums[i]
            streak = 0

        # find duplicates and skip over them
        while i < len(nums) and nums[i] == curr:
            i += 1

        # update streak and move to the next number
        streak += 1
        curr += 1
        res = max(res, streak)
    return res
```

- Time: `O(nlogn)`
- Space: `O(1)`

```python
def longestConsecutive(self, nums: List[int]) -> int:
    numSet = set(nums)
    longest = 0

    for num in numSet:
        # checks if its the start of a sequence
        if (num - 1) not in numSet:
            length = 1
            # checks if there is a next number in the sequence
            while (num + length) in numSet:
                length += 1

            # saves the longest sequence
            longest = max(length, longest)
    return longest
```

- Time: `O(n)`
- Space: `O(n)`

## Example

1. nums = [100, 4, 200, 1, 3, 2]
2. numSet = {1, 2, 3, 4, 100, 200}, longest = 0
3. (1 - 1) = 0 is not in numSet so 1 is the start of the sequence
4. num = 1
   - length = 1: (1 + 1) = 2 is in numSet, so increment length to 2
   - length = 2: (1 + 2) = 3 is in numSet, so increment length to 3
   - length = 3: (1 + 3) = 4 is in numSet, so increment length to 4
   - length = 4: (1 + 4) = 5 is not in numSet, so stop
5. longest = max(4, 0) = 4
6. do the same for the other numbers
7. Longest consecutive subsequence is 4
