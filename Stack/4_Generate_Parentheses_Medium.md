# Generate Parentheses
You are given an integer `n`. Return all well-formed parentheses strings that you can generate with `n` pairs of parentheses.

### Example 1:
```python
Input: n = 1

Output: ["()"]
```

### Example 2:
```python
Input: n = 3

Output: ["((()))","(()())","(())()","()(())","()()()"]
```
You may return the answer in any order.

### Constraints:
- `1 <= n <= 7`

## Explanation
![Image](/Stack/Images/4_Generate_Parentheses_Medium.jpeg)

## Solution
```python
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        res = []
        stack = []

        def backtrack(openN, closedN):
            if openN == closedN == n:
                res.append(''.join(stack))
                return
            if openN < n:
                stack.append('(')
                backtrack(openN + 1, closedN)
                stack.pop()
            if closedN < openN:
                stack.append(')')
                backtrack(openN, closedN + 1)
                stack.pop()
        
        backtrack(0, 0)

        return res
```