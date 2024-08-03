# Longest Repeating Character Replacement
You are given a string `s` consisting of only uppercase english characters and an integer `k`. You can choose up to `k` characters of the string and replace them with any other uppercase English character.

After performing at most k replacements, return the length of the longest substring which contains only one distinct character.

### Example 1:
```python
Input: s = "XYYX", k = 2

Output: 4
```
Explanation: Either replace the 'X's with 'Y's, or replace the 'Y's with 'X's.

### Example 2:
```python
Input: s = "AAABABB", k = 1

Output: 5
```
### Constraints:
- `1 <= s.length <= 1000`
- `0 <= k <= s.length`

## Explanation
A valid window is when the difference between length of the window and the most frequent character is less than or equal to `k`. Sliding window technique can be used to iterate each valid window. If a valid window occurs, the right iterator is moved forward else the left iterator is moved forward.

## Solution
```python
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        count = {}

        l = 0
        maxf = 0

        for r in range(len(s)):
            count[s[r]] = count.get(s[r], 0) + 1
            maxf = max(maxf, count[s[r]])
            if (r - l + 1) - maxf > k:
                count[s[l]] -= 1
                l += 1
        
        return (r - l + 1)
```