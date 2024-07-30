# Valid Anagram
Given two strings `s` and `t`, return true if the two strings are anagrams of each other, otherwise return false.

An anagram is a string that contains the exact same characters as another string, but the order of the characters can be different.

### Example 1:

```
Input: s = "racecar", t = "carrace"

Output: true
```

### Example 2:
```
Input: s = "jar", t = "jam"

Output: false
```
Constraints:

`s` and `t` consist of lowercase English letters.

## Solution 1(Strings)

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        return ''.join(sorted(s)) == ''.join(sorted(t))
```
## Explanation 1
An anagram contains the same set of letters in both words. To check if two words are anagrams, both words can be sorted in ascending manner and can be checked if they are equal or not.

## Solution 2(hashmap/dictionary) Optimised!
```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        smap = {char: s.count(char) for char in set(s)}
        tmap = {char: t.count(char) for char in set(t)}

        return smap == tmap
```
## Explanation 2
A hashmap can be created for both `s` and `t` string can be compared.
