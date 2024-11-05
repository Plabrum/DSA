7. **Kadane's Algorithm (Maximum Sum Subarray)**:  
   A dynamic programming algorithm that finds the contiguous subarray with the maximum sum in an array of numbers by iterating through the array and keeping track of the current sum and the global maximum.

### 7. Kadane's Algorithm (Maximum Sum Subarray)

```python
def kadane(nums):
    max_sum = curr_sum = nums[0]
    for num in nums[1:]:
        curr_sum = max(num, curr_sum + num)
        max_sum = max(max_sum, curr_sum)
    return max_sum
```

11. **Boyer-Moore Algorithm (Majority Finder)**:  
     A linear-time algorithm that finds the majority element (an element that appears more than half the time) by maintaining a candidate and a counter, incrementing the counter when the candidate is matched and decrementing otherwise.

### 11. Boyer-Moore Algorithm (Majority Element Finder)

```python
def boyer_moore(nums):
    candidate, count = None, 0
    for num in nums:
        if count == 0:
            candidate = num
        count += 1 if num == candidate else -1

    return candidate
```
