# Longest Substring Without Repeating Characters
Given a string `s`, find the length of the longest substring without duplicate characters.

A substring is a contiguous sequence of characters within a string.

### Example 1:
```python
Input: s = "zxyzxyz"

Output: 3
```
Explanation: The string "xyz" is the longest without duplicate characters.

### Example 2:
```
Input: s = "xxxx"

Output: 1
```
### Constraints:
- `0 <= s.length <= 1000`
- `s may consist of printable ASCII characters.`

## Solution 1(strings)
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        if not s:
            return 0

        l, r = 0, 1

        sub = s[l]
        longest = 1

        while r < len(s):
            if s[r] not in sub:
                sub += s[r]
                r += 1
            else:
                l += 1
                sub = sub[l:r+1]
            longest = max(longest, len(sub))
        
        return longest
```

## Solution 2(sets)
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        if not s:
            return 0

        l, r = 0, 0

        sub = set()
        longest = 1

        while r < len(s):
            if s[r] not in sub:
                sub.add(s[r])
                r += 1
            else:
                sub.remove(s[l])
                l += 1
            longest = max(longest, r - l)
        
        return longest
```

## Solution 3(sets with optimized loops)
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        if not s:
            return 0

        l, r = 0, 0

        sub = set()
        longest = 1

        while r < len(s):
            while s[r] in sub:
                sub.remove(s[l])
                l += 1
            sub.add(s[r])
            r += 1
            longest = max(longest, r - l)
        
        return longest
```