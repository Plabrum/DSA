## Combined BFS and DFS Algorithm

```python
class Traverse:
    def __init__(self, searchType: str, processNode):
        self.searchType = searchType
        self.processNode = processNode

    def traverse(self, startNode, graph):
        visited = set()  # Keeps track of visited nodes
        stack = [startNode]  # Stack for DFS or Queue for BFS (LIFO/ FIFO based on searchType)

        while stack:
            match self.searchType:
                case 'DFS':
                    node = stack.pop()  # Remove the last element for DFS
                case 'BFS':
                    node = stack.pop(0)  # Remove the first element for BFS

            if node not in visited:
                self.processNode(node)  # Process the current node
                visited.add(node)  # Mark node as visited

                # Add unvisited neighbors to the stack/queue
                for neighbor in graph[node]:
                    if neighbor not in visited:
                        stack.append(neighbor)

```

### 1. **Depth-First Search (DFS)**

DFS is used to explore nodes and edges of a graph or a tree deeply before backtracking. It uses a stack data structure (explicitly or implicitly through recursion).

#### Implementation:

```python
# DFS for a graph
def dfs(graph, start):
    visited = set()  # Set to keep track of visited nodes
    stack = [start]  # Stack for DFS (LIFO)

    while stack:
        node = stack.pop()  # Remove the last element
        if node not in visited:
            print(node, end=" ")  # Process the node
            visited.add(node)  # Mark node as visited
            # Add all unvisited neighbors to the stack
            for neighbor in graph[node]:
                if neighbor not in visited:
                    stack.append(neighbor)

# Example usage:
graph = {
    1: [2, 3],
    2: [4, 5],
    3: [6, 7],
    4: [],
    5: [],
    6: [],
    7: []
}
dfs(graph, 1)  # Output: 1 3 7 6 2 5 4
```

#### Explanation:

- We use a stack to keep track of nodes that need to be explored.
- Starting from the `start` node, we explore each node deeply before backtracking.
- Nodes are marked as visited once they are explored to prevent reprocessing.
- This implementation uses an iterative approach, but it can also be done using recursion.

###### Comments

- Manipulate a stack
- Do operations on a visit
- Add neighbours to the visited set

### 2. **Breadth-First Search (BFS)**

BFS explores all nodes at the present depth level before moving on to nodes at the next depth level. It uses a queue data structure.

#### Implementation:

```python
# BFS for a graph
def bfs(graph, start):
    stack = [start]
    visited = set()
    while stack:
        node = stack.pop(0)
        print(node, end=" ")
        visited.add(node)
        for neighbor in graph[node]:
            if neighbor not in visited:
                stack.append(neighbor)

# Example usage:
graph = {
    1: [2, 3],
    2: [4, 5],
    3: [6, 7],
    4: [],
    5: [],
    6: [],
    7: []
}
bfs(graph, 1)  # Output: 1 2 3 4 5 6 7
```

#### Explanation:

- We use a queue to keep track of nodes that need to be explored. here we use a list and pop left
- Same as DFS just use a LIFO rather than a FIFO

3. **Kahn's Algorithm (Topological Sort)**:  
   A graph-based algorithm for ordering vertices in a Directed Acyclic Graph (DAG) such that for every directed edge `u → v`, vertex `u` appears before `v`. It uses in-degree tracking and a queue to maintain the sort order.

### 3. Kahn's Algorithm (Topological Sort)

```python
from collections import deque, defaultdict

def kahns_algorithm(n, edges):
    in_degree = [0] * n
    adj_list = defaultdict(list)

    for u, v in edges:
        adj_list[u].append(v)
        in_degree[v] += 1

    queue = deque([i for i in range(n) if in_degree[i] == 0])
    topo_sort = []

    while queue:
        node = queue.popleft()
        topo_sort.append(node)

        for neighbor in adj_list[node]:
            in_degree[neighbor] -= 1
            if in_degree[neighbor] == 0:
                queue.append(neighbor)

    return topo_sort if len(topo_sort) == n else []
```

4. **Kruskal's Algorithm (Minimum Spanning Tree)**:  
   A greedy algorithm that finds the minimum spanning tree by sorting edges by weight and adding them to the tree if they don’t form a cycle, using the union-find data structure for cycle detection.

### 4. Kruskal's Algorithm (Minimum Spanning Tree)

```python
def kruskals_algorithm(n, edges):
    parent = list(range(n))

    def find(x):
        if parent[x] != x:
            parent[x] = find(parent[x])
        return parent[x]

    def union(x, y):
        rootX, rootY = find(x), find(y)
        if rootX != rootY:
            parent[rootY] = rootX

    edges.sort(key=lambda x: x[2])  # Sort by weight
    mst = []
    for u, v, weight in edges:
        if find(u) != find(v):
            union(u, v)
            mst.append((u, v, weight))
    return mst
```

5. **Prim's Algorithm (Minimum Spanning Tree)**:  
   A greedy algorithm that grows the minimum spanning tree by starting at an arbitrary node and expanding by adding the cheapest edge that connects the tree to a new vertex.

### 5. Prim's Algorithm (Minimum Spanning Tree)

```python
import heapq

def prims_algorithm(n, edges):
    adj = defaultdict(list)
    for u, v, w in edges:
        adj[u].append((v, w))
        adj[v].append((u, w))

    visited = [False] * n
    min_heap = [(0, 0)]  # (weight, node)
    mst = 0

    while min_heap:
        weight, u = heapq.heappop(min_heap)
        if visited[u]:
            continue
        mst += weight
        visited[u] = True

        for v, w in adj[u]:
            if not visited[v]:
                heapq.heappush(min_heap, (w, v))

    return mst
```

6. **Dijkstra's Algorithm (Shortest Path)**:  
   An algorithm for finding the shortest paths from a source node to all other nodes in a graph with non-negative edge weights. It uses a priority queue to explore nodes in order of their tentative distances.

### 6. Dijkstra's Algorithm (Shortest Path)

```python
import heapq

def dijkstra(n, edges, start):
    adj = defaultdict(list)
    for u, v, w in edges:
        adj[u].append((v, w))

    distances = [float('inf')] * n
    distances[start] = 0
    pq = [(0, start)]

    while pq:
        dist, u = heapq.heappop(pq)
        if dist > distances[u]:
            continue

        for v, w in adj[u]:
            new_dist = dist + w
            if new_dist < distances[v]:
                distances[v] = new_dist
                heapq.heappush(pq, (new_dist, v))

    return distances
```

7. **Hierholzer's Algorithm (Eulerian Circuit)**:  
   An algorithm to find an Eulerian circuit (a cycle that visits every edge exactly once) in a graph. It works by constructing the circuit in parts, starting from any vertex with unused edges and combining partial cycles.

### 8. Hierholzer's Algorithm (Eulerian Circuit)

```python
from collections import defaultdict

def hierholzer(edges):
    adj = defaultdict(list)
    for u, v in edges:
        adj[u].append(v)
        adj[v].append(u)

    stack, circuit = [list(adj.keys())[0]], []

    while stack:
        u = stack[-1]
        if adj[u]:
            v = adj[u].pop()
            adj[v].remove(u)
            stack.append(v)
        else:
            circuit.append(stack.pop())

    return circuit[::-1]
```

10. **Floyd's Cycle Detection Algorithm (Cycle Detection)**:  
     Also known as the "tortoise and hare" algorithm, it detects cycles in a sequence of values by advancing two pointers at different speeds and checking if they eventually meet, indicating a cycle.

### 10. Floyd's Cycle Detection Algorithm

```python
def floyd_cycle_detection(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True
    return False
```
