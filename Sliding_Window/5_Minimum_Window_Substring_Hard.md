# Minimum Window Substring
Given two strings `s` and `t`, return the shortest substring of `s` such that every character in `t`, including duplicates, is present in the substring. If such a substring does not exist, return an empty string `""`.

You may assume that the correct output is always unique.

### Example 1:
```python
Input: s = "OUZODYXAZV", t = "XYZ"

Output: "YXAZ"
```
Explanation: "YXAZ" is the shortest substring that includes "X", "Y", and "Z" from string t.

### Example 2:
```python
Input: s = "xyz", t = "xyz"

Output: "xyz"
```

### Example 3:
```python
Input: s = "x", t = "xy"

Output: ""
```

### Constraints:
- `1 <= s.length <= 1000`
- `1 <= t.length <= 1000`
- `s and t consist of uppercase and lowercase English letters.`

## Solution
```python
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        if len(s) < len(t):
            return ""
        
        if s == t:
            return t

        tMap, window = {}, {}

        for char in t:
            tMap[char] = tMap.get(char, 0) + 1

        have, need = 0, len(tMap)
        minimum = float('inf')
        result = [-1, -1]
        l = 0

        for r in range(len(s)):
            if s[r] in tMap:
                window[s[r]] = window.get(s[r], 0) + 1
                if window[s[r]] == tMap[s[r]]:
                    have += 1

            while have == need:
                if r - l + 1 < minimum:
                    minimum = r - l + 1
                    result = [l, r]

                if s[l] in tMap:
                    window[s[l]] -= 1
                    
                    if window[s[l]] < tMap[s[l]]:
                        have -= 1
                l += 1
        l, r = result
        return s[l:r+1]
```