# 347. Top K Frequent Elements

Given an integer array `nums` and an integer `k`, return the `k` most frequent elements. You may return the answer in any order

- Bucket sort: we will have the count of occurrences of each number as the input and the list of values that match that occurence as the output
  - if there is avlue of 100 in the array, then we would map `[100]` to `1`

## Solution bubble sort (optimal)

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

- Time: `O(n)`
- Space: `O(n)`

## Solution Heap

```python
def topKElement(self, nums: List[int], k: int) -> List[int]:
    # counts the frequency of each number in nums
    count = {}
    for num in nums:
        count[num] = 1 + count.get(num, 0)

    # use min-heap/priority queue
    heap = []
    for num in count.keys():
        # pushes a tuple onto the heap where count[num] is the frequency and num is the number
        heapq.heappush(heap, (count[num], num))

        # ensures the heap never grows larger than k and pops out the least frequent element
        if len(heap) > k:
            heapq.heappop(heap)

    # we get the number value out of the tuple and store it in results
    res = []
    for i in range(k):
        res.append(heapq.heappop(heap)[1])
    return res
```

- Time: `O(nlogk)`: where `n` is the length of the input array `nums` and `k` is the elements in the heap
- Space: `O(n+k)`

## Example

1. `nums = [1, 1, 1, 2, 2, 3]`, `k = 2`
2. `count`: `{1: 3, 2: 2, 3: 1}`
3. `freq`: `[[], [3], [2], [1], [], [], ...]`
4. Iterate over `freq` in reverse

- `i = 3`: `freq[3]` is `[1]`, add `1` to `res`
- `i = 2`: `freq[2]` is `[2]`, add `2` to `res`

5. Now, `res` has `2` elements and `k = 2`, so return `res`
6. returned: `[1, 2]`

## Questions to ask the interviewer

- Can I assume the input array is non-empty?
- Can there be negative numbers or are all non-negative integers?
- Are the elements in nums sorted or bounded?
- How should I handle ties in frequency? Does it matter which one I return?
- Can we assume k is in the range of unique elements in the array?
- How should I handle the case where k = 0?
