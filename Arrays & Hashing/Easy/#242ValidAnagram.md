# 242. Valid Anagram

Given 2 strings `s` and `t`, return true if `t` is an anagram of `s` and false otherwise
- Goal: Compare the two strings by getting the occurence of each letter in each string

## Hashmap solution

```python
def isAnagram(self, s: str, t: str) -> bool:
    # checks if both strings have the same amount of letters
    if len(s) != len(t):
        return False
    
    # use hashmap for both strings
    countS, countT = {}, {}

    # iterate through both strings
    for i in range(len(s)):
        # adds 1 to the value of each letter in the hashmap
        countS[s[i]] = 1 + countS.get(s[i], 0)
        countT[t[i]] = 1 + countT.get(t[i], 0)

    # checks if the hashmaps are equal which means they are anagrams of each other
    return countS == countT
```
- Time: `O(n)`
- Space: `O(n)`

## Sorting solution
```python
def isAnagram(self, s: str, t: str) -> bool:
    # sorts the two strings and compares them
    return sorted(s) == sorted(t)
```
- Time: `O(nlogn)`
- Space: `O(n)`

## Example

1. `s = "anagram"`, `t = "nagaram"`
2. `7` = `7`
3. `countS` and `countT` are both empty
4. `countS['a'] = 1 + 0`, `countT['n'] = 1 + 0`
5. After going through the entire string: `countS = {'a': 2, 'n': 1, 'g': 1, 'r': 1, 'm': }`, `countT = {'a': 2, 'n': 1, 'g': 1, 'r': 1, 'm': }`
6. countS == countT
7. return `True`