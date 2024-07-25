# 125. Valid Palindrome

A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphasnumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers. Given a string `s`, return `true` if it is a palindrome, or `false` otherwise

## "Cheating" solution (uses built-in python features)
```python
def isPalindrome(self, s: str) -> bool:
    # new string
    newStr = ""

    # iterates through the string
    for c in s:
        # checks if the letter is an alphanumeric character and adds it to the new string as lowercased
        if c.isalnum():
            newStr += c.lower()
    # checks if the new string and new string backwards are equal
    return newStr == newStr[::-1]
```
Time: `O(n^2)`
Space: `O(n)`

## Two pointer solution
```python
def isPalindrome(self, s: str) -> bool:
    # set a left pointer to 0 and a right pointer to the end of the string
    l, r = 0, len(s) - 1

    # iterate through til l and r come together or two letters are not equal
    while l < r:
        # checks if the character at the left pointer is not an alphanumeric character, increment the pointer by 1
        while l < r and not self.alphaNum(s[l]):
            l += 1

        # checks if the character at the right pointer is not an alphanumeric character, decrement the pointer by 1
        while r > l and not self.alphaNum(s[r]):
            r -= 1

        # checks if the letters at each pointer are equal, if not then return false
        if s[l].lower() != s[r].lower():
            return False

        # increment the left pointer and decrement the right pointer by 1
        l, r = l + 1, r - 1
    return True

def alphaNum(self, c):
    # checks if the character is an alphanumeric character by checking if the character is inbetween the ASCII values of 'A' and 'Z', 'a' and 'z', and '0' and '9'
    return (ord('A') <= ord(c) <= ord('Z') or
            ord('a') <= ord(c) <= ord('z') or
            ord('0') <= ord(c) <= ord('9'))
```

## Example

1. `s = "race a car"`
2. `l = 0` and `r = 10 - 1 = 9`
3. `l < r` and `r > l` and `s[l] = r` and `s[r] = r` are both alphanumeric characters
4. `l = 1` and `r = 8`
5. `l` and `r` check for the next couple of characters and all are equal
6. Now we have `l = 3` and `r = 6`
7. `s[l] = e` but `s[r] = ' '` so decrement `r` by 1
8. `l = 3` and `r = 5`
9. `s[l] = e` and `s[r] = a` and both are not equal
10. return `False`