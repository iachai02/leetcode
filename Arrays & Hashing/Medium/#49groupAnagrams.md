# 49. Group Anagrams

Given an array of strings `strs`, group the anagrams together. You can return the answer in any order. An anagram is a word or phrase formed by rearranging the letters of a different word of phrase, typically using all the original letters exactly once

- Sorting: we can try sorting everything in the list of strings given, but the time complexity would be `O(m*nlogn)`
- Hashmap: we know that there are only lowercased letters involved so that means there are only 26 letters being used. We can count the occurences of each letter as the key for our hashmap and the list of anagrams as the value

```python
def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
    res = defaultdict(list)

    # iterate through the list of strings
    for s in strs:
        # create an array for the occurences of each letter
        count = [0] * 26

        # iterate through each letter in the string
        for c in s:

            # ord(c) - ord("a") -> "a" - "a" = 0, "z" - "a" = 25 -> indexes
            # counting how many characters we have in the string "s"
            count[ord(c) - ord("a")] += 1

        # adds the tuple of letters counted as the key and the string as the value
        res[tuple(count)].append(s)

    # returns the string values of the dictionary
    return res.values()
```

- Time: `O(m*n)` where `m` is the length of the list of strings and `n` is the average length of each string in the list of strings
- Space: `O(m*n)`
