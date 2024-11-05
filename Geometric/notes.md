2. **Line Sweep (Trick)**:  
   The line sweep (or "sweep line") trick is a geometric algorithm technique used to solve problems involving intervals or points in 1D or 2D space. The idea is to imagine a line sweeping across the space (typically horizontally or vertically), processing events in a sorted order (e.g., endpoints of intervals, points of interest). It is often used in problems like finding overlapping intervals, computing the union of rectangles, or closest pair of points. By organizing events into a sorted sequence and handling them as the line passes through, the trick reduces the problem's complexity.

### 2. Line Sweep (Trick)

The line sweep algorithm is used for finding the number of overlapping intervals.

```python
def countOverlappingIntervals(intervals):
    events = []
    for start, end in intervals:
        events.append((start, 1))  # 1 indicates interval starts
        events.append((end, -1))   # -1 indicates interval ends

    events.sort()
    active, max_overlap = 0, 0
    for _, event in events:
        active += event
        max_overlap = max(max_overlap, active)
    return max_overlap
```

14. **Kuhn-Munkres/Hungarian Algorithm (Assignment Optimization)**:  
    An algorithm used to solve the assignment problem by finding the optimal matching of agents to tasks in a weighted bipartite graph, minimizing the total cost or maximizing the total benefit.

### 14. Kuhn-Munkres (Hungarian Algorithm)

```python
import numpy as np

def hungarian_algorithm(cost_matrix):
    from scipy.optimize import linear_sum_assignment
    row_ind, col_ind = linear_sum_assignment(cost_matrix)
    return cost_matrix[row_ind, col_ind].sum(), list(zip(row_ind, col_ind))
```
