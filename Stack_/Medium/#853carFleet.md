# 853. Car Fleet

There are `n` cars at given miles away from the starting mile 0, traveling to reach the mile `target`. You are given two integer array `position` and `speed`, both of length `n`, where `position[i]` is the starting mile of the `ith` car and `speed[i]` is the speed of the `ith` car in miles per hour. A car cannot pass another car, but it can catch up and then travel next to it at the speed of the slower car. A car fleet is a car of cars driving next to each other. The speed of the car fleet is the minimum array of any car in the fleet. If a car catches up to a car fleet at the mile `target`, it will still be considered as part of the car fleet. Return the number of car fleets that will arrive at the destination.

## Solution

```python
def carFleet(self, target: int, position: list[int], speed: list[int]) -> int:
    # creates a list of pairs where each pair contains the position and speed of a car
    pair = [[p, s] for p, s in zip(position, speed)]
    stack = []

    # go through the reversed sorted pairs to iterate from the car closest to the target to teh one furthest from the target
    for p, s in sorted(pair)[::-1]:
        # add the time it takes to reach the destination to the stack
        stack.append((target - p) / s)

        # if the car's time is less than or equal to the previous car's time, it means the car will join the same fleet as the previous car
        if len(stack) >= 2 and stack[-1] <= stack[-2]:
            stack.pop()
    return len(stack)
```

- Time: `O(nlogn)`
- Space: `O(n)`

## Example

1. target = 12, position = [10, 8, 0, 5, 3], speed = [2, 4, 1, 1, 3]
2. pair = [[10, 2], [8, 4], [0, 1], [5, 1], [3, 3]]
3. sorted(pair) = [[0, 1], [3, 3], [5, 1], [8, 4], [10, 2]] and we are going through this in reverse order
4. 12 - 10 / 2 = 1, stack = [1]
5. 12 - 8 / 4 = 1, stack = [1, 1], len(stack) = 2 and 1 <= 1 so stack = [1]
6. 12 - 5 / 1 = 7, stack = [1, 7], 7 > 1
7. 12 - 3 / 3 = 3, stack = [1, 7, 3], len(stack) = 3 and 3 <= 7 so stack = [1, 7]
8. 12 - 0 / 1 = 12, stack = [1, 7, 12], 12 > 7
9. return len(stack) = 3
