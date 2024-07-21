# Encode and Decode Strings
Design an algorithm to encode a list of strings to a single string. The encoded string is then decoded back to the original list of strings.

Please implement `encode` and `decode`

### Example 1:
```python
Input: ["neet","code","love","you"]

Output:["neet","code","love","you"]
```
### Example 2:
```python
Input: ["we","say",":","yes"]

Output: ["we","say",":","yes"]
```
### Constraints:
- `0 <= strs.length < 100`
- `0 <= strs[i].length < 200`
- `strs[i] contains only UTF-8 characters.`

## Solution
```python
class Solution:

    def encode(self, strs: List[str]) -> str:
        encode = ""

        for i in range(len(strs)):
            encode += "#{" + str(len(strs[i])) + "}" + strs[i]
        
        return encode

    def decode(self, s: str) -> List[str]:
        res = []
        i, j = 0, 1

        while j < len(s):
            if s[i] == '#' and s[j] == '{':
                k = j + 1
                while s[k] != '}':
                    k += 1
                length = int(s[j + 1:k])
                res.append(s[k + 1:k + 1 + length])
                i = k + 1 + length
                j = i + 1

        return res
```
## Explanation
All elements of the array can be added to the string `encode`. `#{n}` is added in front of every string to denote the start and length of the string following it. In `decode` three iterators are used to keep the check of `#`, `{`, and `}` to verify the start and length of the string. 