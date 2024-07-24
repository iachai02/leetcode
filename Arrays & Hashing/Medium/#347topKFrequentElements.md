# 347. Top K Frequent Elements

Given an integer array `nums` and an integer `k`, return the `k` most frequent elements. You may return the answer in any order
- Bucket sort: we will have the count of occurrences of each number as the input and the list of values that match that occurence as the output
    - if there is avlue of 100 in the array, then we would map `[100]` to `1`
```python
def topKFrequent(self, nums: List[int], k: int) -> List[int]:
    # dictionary to count the frequency of each element
    count = {}

    # list of empty lists to group numbers by their frequencies
    freq = [[] for i in range(len(nums) + 1)]

    # count the frequency of each number in nums
    for n in nums:
        count[n] = 1 + count.get(n, 0)

    # groups the numbers by their frequencies in the freq list 
    for n, c in count.items():
        freq[c].append(n)

    # list of results
    res = []

    # iterate through the length of the frequency list in reverse order
    for i in range(len(freq) - 1, 0, -1):
        for n in freq[i]:
            res.append(n)
            if len(res) == k:
                return res
```
Time: `O(n)`
Space: `O(n)`

# Example

1. `nums = [1, 1, 1, 2, 2, 3]`, `k = 2`
2. `count`: `{1: 3, 2: 2, 3: 1}`
3. `freq`: `[[], [3], [2], [1], [], [], ...]`
4. Iterate over `freq` in reverse
    a. `i = 3`: `freq[3]` is `[1]`, add `1` to `res`
    b. `i = 2`: `freq[2]` is `[2]`, add `2` to `res`
5. Now, `res` has `2` elements and `k = 2`, so return `res`
6. returned: `[1, 2]`