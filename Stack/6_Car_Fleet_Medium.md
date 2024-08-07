# Car Fleet
There are `n` cars traveling to the same destination on a one-lane highway.

You are given two arrays of integers `position` and `speed`, both of length `n`.
- `position[i]` is the position of the `ith` car (in miles)
- `speed[i]` is the speed of the `ith` car (in miles per hour)

The **destination** is at position `target` miles.

A car can **not** pass another car ahead of it. It can only catch up to another car and then drive at the same speed as the car ahead of it.

A **car fleet** is a non-empty set of cars driving at the same position and same speed. A single car is also considered a car fleet.

If a car catches up to a car fleet the moment the fleet reaches the destination, then the car is considered to be part of the fleet.

Return the number of **different car fleets** that will arrive at the destination.

### Example 1:
```python
Input: target = 10, position = [1,4], speed = [3,2]

Output: 1
```
Explanation: The cars starting at 1 (speed 3) and 4 (speed 2) become a fleet, meeting each other at 10, the destination.

### Example 2:
```python
Input: target = 10, position = [4,1,0,7], speed = [2,2,1,1]

Output: 3
```
Explanation: The cars starting at 4 and 7 become a fleet at position 10. The cars starting at 1 and 0 never catch up to the car ahead of them. Thus, there are 3 car fleets that will arrive at the destination.

### Constraints:
- `n == position.length == speed.length.`
- `1 <= n <= 1000`
- `0 < target <= 1000`
- `0 < speed[i] <= 100`
- `0 <= position[i] < target`
- All the values of `position` are **unique**.

## Explanation
The solution can be framed with respect to `position` and `time to finish`. Given the situation, a car cannot overtake which implies, the nearer the car is to the target the faster it should finish. If the cars are sorted in reverse order based on their position. The time calculated to reach the target should be increasing in an ideal scenario where cars do not overtake each other. If any car overtake, the time taken to reach the target will be lower than the previous car(the car ahead of it in position).

It can be either solved with stacks or a counter variable. 

### Stacks
```python
position        = [4, 2, 0, 7]
speed           = [2, 2, 1, 1]
target          = 10

# Reverse sorted distance, speed pair
pair            = [(7,1), (4,2), (2, 2), (0,1)]
time_to_reach   = []

for pos, spd in pair:
    time = (target - pos) / spd
    time_to_reach.append(time)
    if len(time_to_reach) > 1 and time_to_reach[-1] >= time_to_reach[-2]:
        time_to_reach.pop()

# Time to reach = (target - position) / speed
# If the last element is less than or equal to the second last element, the last element will be popped.
# 
# ---1st iteration---
# Time to reach = (10 - 7) / 1 == 3 
# time_to_reach.append(3)
# time_to_reach = [3]
# 
# ---2nd iteration---
# Time to reach = (10 - 4) / 2 == 3
# time_to_reach.append(3)
# time_to_reach[-1] >= time_to_reach[-2]
# 3 >= 3
# time_to_reach.pop()
# time_to_reach = [3]
# 
# ---3rd iteration---
# Time to reach = (10 - 2) / 2 == 4
# time_to_reach.append(4)
# time_to_reach = [3, 4]
# 
# ---4th iteration---
# Time to reach = (10 - 0) / 1 == 10
# time_to_reach.append(10)
# time_to_reach = [3, 4, 10]
# 
# Hence there are 3 unique fleets.
```
Using stacks we can append the `time to reach` of the `ith` car, if it is greater than or equal to the previous element it will be removed.

### Counter Variable
This approach is same till calculating time to approach for all positions. A counter variable `fleet` can be initialized as `0`. It will keep the count whenever the `ith` value is bigger than the previous max values.


## Solution 1 (Stacks)
```python
class Solution:
    def carFleet(self, target: int, position: List[int], speed: List[int]) -> int:
        pair = [(p, s) for p, s in zip(position, speed)]
        pair.sort(reverse=True)

        stack =[]
        for p, s in pair:
            time = (target - p) / s
            stack.append(time)
            if len(stack) > 1 and stack[-1] <= stack[-2]:
                stack.pop()

        return len(stack)
```

## Solution 2 (Counter Variable)
```python
class Solution:
    def carFleet(self, target: int, position: List[int], speed: List[int]) -> int:
        cars = sorted(zip(position, speed), reverse=True)
        fleets = 0
        time_to_reach = 0

        for pos, spd in cars:
            time = (target - pos) / spd
            if time > time_to_reach:
                fleets += 1
                time_to_reach = time
        
        return fleets
```