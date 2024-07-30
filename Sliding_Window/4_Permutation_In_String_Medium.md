# Permutation in String
You are given two strings `s1` and `s2`.

Return true if `s2` contains a permutation of `s1`, or false otherwise. That means if a permutation of `s1` exists as a substring of `s2`, then return true.

Both strings only contain lowercase letters.

### Example 1:
```python
Input: s1 = "abc", s2 = "lecabee"

Output: true
```

Explanation: The substring "cab" is a permutation of "abc" and is present in "lecabee".

Example 2:
```python
Input: s1 = "abc", s2 = "lecaabee"

Output: false
```

### Constraints:
- `1 <= s1.length, s2.length <= 1000`

## Explanation
![Image](/Sliding_Window/Images/permutation.jpeg)

## Solution
```python
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        l, r = 0, len(s1) - 1
        sub = {char: s1.count(char) for char in set(s1)}
        window = {char: s2[l:r+1].count(char) for char in set(s2[l:r+1])}
        if sub == window:
                return True
        l += 1
        r +=1
        while r < len(s2):
            if window[s2[l-1]] == 1:
                del window[s2[l-1]]
            else:
                window[s2[l-1]] -= 1
            try:
                window[s2[r]] += 1
            except:
                window[s2[r]] = 1
            l += 1
            r +=1
            
            if window == sub:
                return True
        return False
```
