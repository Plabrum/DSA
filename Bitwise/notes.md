Here’s a concise cheat sheet that covers common LeetCode sub-problems involving bitwise operations, backtracking, sliding windows, and generating all subarrays.

---

### **1. Bitwise Operations**

#### **Common Operators**

- **AND (`&`)**: Both bits are 1 → `a & b`
- **OR (`|`)**: At least one bit is 1 → `a | b`
- **XOR (`^`)**: One bit is 1, the other is 0 → `a ^ b`
- **NOT (`~`)**: Inverts all bits → `~a`
- **Left Shift (`<<`)**: Shifts bits left, adding zeros → `a << n`
- **Right Shift (`>>`)**: Shifts bits right, preserving the sign → `a >> n`

#### **Examples**

- **Check if a number is even or odd**:

  ```python
  if num & 1 == 0:  # Even
  if num & 1 == 1:  # Odd
  ```

- **Get the ith bit**:

  ```python
  (num >> i) & 1
  ```

- **Set the ith bit**:

  ```python
  num |= (1 << i)
  ```

- **Clear the ith bit**:

  ```python
  num &= ~(1 << i)
  ```

---

### **2. Backtracking**

#### **Template for Backtracking**

```python
def backtrack(path, options):
    if base_case:
        result.append(path[:])
        return

    for option in options:
        # Make a choice
        path.append(option)

        # Recurse
        backtrack(path, options)

        # Undo the choice
        path.pop()
```

#### **Examples**

- **Permutations**:

  ```python
  def permute(nums):
      result = []
      def backtrack(path, options):
          if len(path) == len(nums):
              result.append(path[:])
              return
          for i in range(len(options)):
              backtrack(path + [options[i]], options[:i] + options[i+1:])
      backtrack([], nums)
      return result
  ```

- **Combinations**:

  ```python
  def combine(n, k):
      result = []
      def backtrack(start, comb):
          if len(comb) == k:
              result.append(comb[:])
              return
          for i in range(start, n + 1):
              comb.append(i)
              backtrack(i + 1, comb)
              comb.pop()
      backtrack(1, [])
      return result
  ```

---

### **3. Sliding Window**

#### **Template for Sliding Window**

```python
def sliding_window(nums, k):
    left = 0
    for right in range(len(nums)):
        # Expand the window

        # Shrink the window if it exceeds size k
        if right - left + 1 > k:
            left += 1
```

#### **Examples**

- **Find the maximum sum of k consecutive elements**:

  ```python
  def max_sum_subarray(nums, k):
      max_sum = float('-inf')
      current_sum = 0
      left = 0

      for right in range(len(nums)):
          current_sum += nums[right]

          if right - left + 1 == k:
              max_sum = max(max_sum, current_sum)
              current_sum -= nums[left]
              left += 1

      return max_sum
  ```

- **Find all anagrams in a string**:

  ```python
  def find_anagrams(s, p):
      from collections import Counter
      result = []
      p_count = Counter(p)
      s_count = Counter()
      left = 0

      for right in range(len(s)):
          s_count[s[right]] += 1

          if right - left + 1 > len(p):
              if s_count[s[left]] == 1:
                  del s_count[s[left]]
              else:
                  s_count[s[left]] -= 1
              left += 1

          if s_count == p_count:
              result.append(left)

      return result
  ```

---

### **4. Generating All Subarrays**

#### **Iterative Approach**

- **All subarrays**:

  ```python
  def all_subarrays(nums):
      result = []
      for i in range(len(nums)):
          for j in range(i, len(nums)):
              result.append(nums[i:j+1])
      return result
  ```

#### **Examples**

- **Sum of all subarrays**:

  ```python
  def sum_of_subarrays(nums):
      total_sum = 0
      for i in range(len(nums)):
          for j in range(i, len(nums)):
              total_sum += sum(nums[i:j+1])
      return total_sum
  ```

- **Maximum sum of subarrays (Kadane's Algorithm)**:

  ```python
  def max_subarray(nums):
      max_sum = nums[0]
      current_sum = nums[0]

      for i in range(1, len(nums)):
          current_sum = max(nums[i], current_sum + nums[i])
          max_sum = max(max_sum, current_sum)

      return max_sum
  ```

---

This cheat sheet provides useful snippets for common sub-problems, which you can tweak as needed during coding practice.
