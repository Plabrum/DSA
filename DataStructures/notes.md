---

### Approach: Prefix Sum with Hash Map

We can solve this problem efficiently by using a hash map to store the difference between the target and the current element (prefix sum logic). The key idea is to traverse the array and for each element, check if its complement (i.e., `target - nums[i]`) exists in the hash map. If it does, we return the indices. Otherwise, store the current element with its index in the hash map.

### Algorithm:

1. Initialize an empty hash map `prefix_sums` to store the complement and its index.
2. Traverse the array `nums`:
   - For each element `nums[i]`, calculate `complement = target - nums[i]`.
   - If `complement` is already in the hash map, return the indices `[prefix_sums[complement], i]`.
   - Otherwise, add `nums[i]` to the hash map with its index `i`.
3. If no solution is found, return an empty list (though the problem guarantees one solution).

---

### Prefix Sum

```python
def two_sum(nums, target):
    prefix_sums = {}  # Hash map to store prefix sums (complements)

    for i, num in enumerate(nums):
        complement = target - num

        if complement in prefix_sums:
            return [prefix_sums[complement], i]

        prefix_sums[num] = i  # Store the number with its no

    return []

# Example usage:
nums = [2, 7, 11, 15]
target = 9
print(two_sum(nums, target))  # Output: [0, 1]
```

## Base Algs (if they're really mean)

Min-Heap Implementation:

class MinHeap:
def **init**(self):
self.heap = []

```python
def _parent(self, index):
    return (index - 1) // 2

def _left_child(self, index):
    return 2 * index + 1

def _right_child(self, index):
    return 2 * index + 2

def _swap(self, i, j):
    self.heap[i], self.heap[j] = self.heap[j], self.heap[i]

def _heapify_up(self, index):
    parent_index = self._parent(index)
    if index > 0 and self.heap[index] < self.heap[parent_index]:
        self._swap(index, parent_index)
        self._heapify_up(parent_index)

def _heapify_down(self, index):
    left_index = self._left_child(index)
    right_index = self._right_child(index)
    smallest = index

    if left_index < len(self.heap) and self.heap[left_index] < self.heap[smallest]:
        smallest = left_index
    if right_index < len(self.heap) and self.heap[right_index] < self.heap[smallest]:
        smallest = right_index

    if smallest != index:
        self._swap(index, smallest)
        self._heapify_down(smallest)

def push(self, item):
    self.heap.append(item)
    self._heapify_up(len(self.heap) - 1)

def pop(self):
    if len(self.heap) == 0:
        raise IndexError("Heap is empty")
    if len(self.heap) == 1:
        return self.heap.pop()

    root = self.heap[0]
    # Move the last element to the root and heapify down
    self.heap[0] = self.heap.pop()
    self._heapify_down(0)
    return root

def peek(self):
    if len(self.heap) == 0:
        raise IndexError("Heap is empty")
    return self.heap[0]

def __str__(self):
    return str(self.heap)
```
