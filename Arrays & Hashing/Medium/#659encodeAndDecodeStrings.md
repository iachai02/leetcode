# 659. Encode and Decode Strings

Design an algorithm to encode a list of strings to a string. The encoded string is then sent over the network and is decoded back to the original list of strings.
- Create a way to separate the strings when decoding. One way to do so is to add the number of letters in the string followed by a special character `#` before a word to know when a new word begins and how many letters are in that new word

```python
def encode(self, strs: List[str]) -> str:
    # result string
    res = ""

    # iterate through the list of strings
    for s in strs:
        # get the length of the string + # + the string itself
        res += str(len(s)) + "#" + s
    return res

def decode(self, s: str) -> List[str]:
    # store the decoded strings
    res = []

    # pointer to traverse the encoded string
    i = 0

    # traverse through the encoded string
    while i < len(s):
        j = i
        
        # advances j to the position of #
        while s[j] != "#":
            j += 1
        
        # gets the length of the next string
        length = int(s[i:j])

        # moves past the # character
        i = j + 1

        # define the end position of the actual string
        j = i + length

        # i:j is the decoded string and appended to result list
        res.append(s[i:j])

        # i is updated j to continue the process
        i = j
    return res
```
- Time (encode): `O(n + m)`
- Space (encode): `O(m)`

- Time (decode): `O(m)`
- Space (decode): `O(m)`

## Example

1. `strs = ["lint", "code", "love", "you"]`
2. Iterate through the strings starting with "lint"
3. return `res = "4#lint4#code4#love4#you"`

1. `s = "4#lint4#code4#love4#you"`
2. `j = i = 0`
3. `j = 1` (where the first `#` is)
4. `length = int(s[0:1]) = int("4") = 4`
5. `i = j + 1 = 2`
6. `j = i + length = 2 + 4 = 6`
7. `res.append(s[2:6])` -> `res.append("lint")`
8. Do that for the rest of the words
9. return `res = ["lint", "code", "love", "you"]`