# 217. Contains Duplicate

Given an integer array "nums", return true if any value appears at least twice in the array, and return false if every element is distinct.
- Brute force: start with the first number and compare every number with a different number in the array to see if any are equal.
    - Complexity: `O(n^2)`
    - Space: `O(1)`

```python
def containsDuplicate(self, nums: List[int]) -> bool:
    # use hashset because we only care about if a number appears more than once
    hashset = Set()

    # iterate through the list of numbers
    for n in nums:
        # while iterating, if a number is already in the hashset, that means that number appeared again, so return true
        if n in hashset:
            return True

        # continually add each number from the list to the hashset
        hashset.add(n)
    return False
```
- Time: `O(n)`
- Space: `O(n)`