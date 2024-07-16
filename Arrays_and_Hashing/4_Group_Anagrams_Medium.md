# Anagram Groups
Given an array of strings strs, group all anagrams together into sublists. You may return the output in any order.

An anagram is a string that contains the exact same characters as another string, but the order of the characters can be different.

### Example 1:
```
Input: strs = ["act","pots","tops","cat","stop","hat"]

Output: [["hat"],["act", "cat"],["stop", "pots", "tops"]]
```

### Example 2:
```
Input: strs = ["x"]

Output: [["x"]]
```

### Example 3:
```
Input: strs = [""]

Output: [[""]]
```

### Constraints:
- `1 <= strs.length <= 1000.`
- `0 <= strs[i].length <= 100`
- `strs[i] is made up of lowercase English letters.`

## Solution
```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        str_to_root = {}
        nested_arr = []
        nest_iter = -1
        for i, sub in enumerate(strs):
            root = ''.join(sorted(sub))
            if root in str_to_root:
                nested_arr[str_to_root[anagram]].append(sub)
            else:
                nest_iter += 1
                str_to_root[anagram] = nest_iter
                nested_arr.append([sub])

        return sorted(nested_arr, key=len)
```

## Explanation
`root`: sorts the string in ascending order, example: `"cat" --> "act"`

`str_to_root`: Saves the nested array index and root

`nested_arr`: Groups anagrams together

`nest_iter`: Nested array iterator

1. Iteration 1: [`"act"`,"pots","tops","cat","stop","hat"]
- `root=act`
- `"act"` not in `str_to_arr`
- `str_to_root = {'act': 1}`
- `nested_arr = [['act']]`

2. Iteration 2: ["act",`"pots"`,"tops","cat","stop","hat"]
- `root=opst`
- `"opst"` not in `str_to_arr`
- `str_to_root = {'act': 1, 'opst': 2}`
- `nested_arr = [['act'], ['pots']]`

3. Iteration 3: ["act","pots",`"tops"`,"cat","stop","hat"]
- `root=opst`
- `"opst"` in `str_to_arr`
- `nested_arr = [['act'], ['pots', 'tops']]`

4. Iteration 4: ["act","pots","tops",`"cat"`,"stop","hat"]
- `root=act`
- `"act"` in `str_to_arr`
- `nested_arr = [['act', 'cat'], ['pots', 'tops']]`

5. Iteration 5: ["act","pots","tops","cat",`"stop"`,"hat"]
- `root=opst`
- `"opst"` in `str_to_arr`
- `nested_arr = [['act', 'cat'], ['pots', 'tops', 'stop']]`

6. Iteration 6: ["act","pots","tops","cat","stop",`"hat"`]
- `root=aht`
- `"aht"` not in `str_to_arr`
- `str_to_root = {'act': 1, 'opst': 2, 'aht': 3}`
- `nested_arr = [['act', 'cat'], ['pots', 'tops', 'stop'], ['hat']]`

`return sorted(nested_arr, key=len) #returns sorted nested array based on sub-array lengt h`