# 139. Word Break

Given a string `s` and a dictionary of strings `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words. Note that the same word in the dictionary may be reused multiple times in the segmentation.

## Solution

```python
def wordBreak(self, s: str, wordDict: List[str]):
    # the first true is the base case and the rest are falses at each letter
    # if the last letter is true, then that means we were able to segment the words
    dp = [True] + [False] * len(s)

    # checks each letter
    for i in range(1, len(s) + 1):
        # goes through the word dictionary
        for w in wordDict:
            # checks if the starting index is a potential word segment
            start = i - len(w)

            # i represents the length of the prefix we are trying to check for segmentabilitity
            # this ensures that the length of the word is in the bounds, checks if the up to the start position, the string can be split into valid words from wordDict, and checks if the actual word matches the word in wordDict
            if start >= 0 and dp[start] and s[start:i] == w:
                dp[i] = True
                break
        return dp[-1]
```

- Time: `O(n*m*k)`, where n is the length of the string s, m is the number of words in wordDict, and k is the average length of a word in wordDict (substring comparison)
- Space: `O(n*m*k)`
