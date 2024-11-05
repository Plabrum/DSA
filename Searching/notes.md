### 3. **Sliding Window**

The sliding window technique is used for problems involving subarrays or substrings. It efficiently finds or optimizes a solution over a contiguous segment of an array or string.

#### Implementation: Maximum Sum of Subarray of Size `k`

```python
# Sliding window to find the maximum sum of a subarray of size k
def max_sum_subarray(arr, k):
    n = len(arr)
    if n < k:
        return -1  # If the array is smaller than k

    max_sum = sum(arr[:k])
    current_sum = max_sum

    for i in range(k, n):
        current_sum += arr[i] - arr[i - k]  # Slide the window to the right
        max_sum = max(max_sum, current_sum)  # Update max sum if necessary

    return max_sum

# Example usage:
arr = [1, 8, 30, -5, 20, 7]
k = 3
print(max_sum_subarray(arr, k))  # Output: 45 (8 + 30 + 7)
```

#### Explanation:

- Remember early return if n < k
- We first calculate the sum of the initial window of size `k`.
- Then, for each subsequent element, we adjust the sum by subtracting the element going out of the window and adding the new element.
- This allows us to compute the sum in `O(1)` time for each shift, leading to an overall time complexity of `O(n)`.

### 4. **Binary Search**

Binary search is used to efficiently find a target value within a sorted array. It repeatedly divides the search interval in half.

#### Implementation:

```python
# Binary search to find an element in a sorted array
def binary_search(arr, target):
    left, right = 0, len(arr) - 1

    while left <= right:
        mid = left + (right - left) // 2  # Avoid potential overflow
        if arr[mid] == target:
            return mid  # Target found at index mid
        elif arr[mid] < target:
            left = mid + 1  # Search in the right half
        else:
            right = mid - 1  # Search in the left half

    return -1  # Target not found

# Example usage:
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]
target = 4
print(binary_search(arr, target))  # Output: 3 (index of element 4)
```

#### Explanation:

- Use left and right pointers
- ensure to use integer division
- ensure to actually index to lookup equality

These are concise implementations and explanations for DFS, BFS, Sliding Window, and Binary Search. Let me know if you'd like to dive deeper into any of these or explore their variations!
