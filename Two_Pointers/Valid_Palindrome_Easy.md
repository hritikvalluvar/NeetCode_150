# Valid Palindrome
Given a string `s`, return `true` if it is a palindrome, otherwise return `false`.

A palindrome is a string that reads the same forward and backward. It is also case-insensitive and ignores all non-alphanumeric characters.

### Example 1:
```python
Input: s = "Was it a car or a cat I saw?"

Output: true
```
Explanation: After considering only alphanumerical characters we have "wasitacaroracatisaw", which is a palindrome.

### Example 2:
```python
Input: s = "tab a cat"

Output: false
```
Explanation: "tabacat" is not a palindrome.

### Constraints:
- `1 <= s.length <= 1000`
- `s is made up of only printable ASCII characters.`

## Solution
```python
import re

class Solution:
    def isPalindrome(self, s: str) -> bool:
        s = re.sub(r'[^a-zA-Z0-9]', '', s).strip().lower()
        n = len(s)

        for i in range(0, n//2):
            if s[i] != s[n-1-i]:
                return False
        return True
```

## Explanation
All white spaces are removed, lowercase is applied and filter is applied to keep only alphabetic numerical characters. Characters from left to right and right to left are compared till the mid-point. If they are not same `false` is returned, else `true`. 