# 🧭 Dijkstra — Shortest Path in a Weighted Graph

## 🔍 What is the problem?

The goal of this problem is to find the **minimum cost (shortest distance)** path
from **vertex 1** to **vertex n** in a **weighted undirected graph**.

In simpler terms:

👉 “What is the minimum sum of edge weights required to go from vertex 1 to vertex n, and which path should be taken?”

---

## 📥 Input Description

Format:

```
n m 
a1 b1 w1 
a2 b2 w2 
...
am bm wm
```

| Symbol   | Meaning                           |
| -------- | --------------------------------- |
| **n**    | Number of vertices (2 ≤ n ≤ 10⁵)  |
| **m**    | Number of edges (0 ≤ m ≤ 10⁵)     |
| **a, b** | Two vertices connected by an edge |
| **w**    | Weight of that edge (1 ≤ w ≤ 10⁶) |

The graph may contain **multiple edges between two vertices** and **loops**.

---

## 📤 Output Description

* If **no path** exists from `1 → n`, print **-1**
* Otherwise, print the **shortest path** (sequence of vertices)

---

## 🧠 Nature of the Problem

This is a **Single Source Shortest Path (SSSP)** problem with **positive edge weights**.

* If all weights were equal (e.g., = 1), BFS would work.
* But weights vary from **1 to 10⁶**, so the best algorithm is:

### ✅ Dijkstra’s Algorithm

---

## ⚙️ Summary of Dijkstra’s Algorithm

Dijkstra follows a **Greedy approach**:

1. Start from vertex **1**
2. At each step, pick the vertex with the **smallest distance**
3. Relax all its neighbors — update their distance if a shorter path is found
4. Continue until reaching **vertex n**

---

## 🧩 Graph Representation (Adjacency List)

Example:

```
1 → (2, 2), (4, 1)
2 → (1, 2), (3, 4), (5, 5)
4 → (1, 1), (3, 3)
3 → (2, 4), (4, 3), (5, 1)
5 → (2, 5), (3, 1)
```

---

## 🧮 Variables

| Variable    | Description                                                            |
| ----------- | ---------------------------------------------------------------------- |
| **dist[i]** | Minimum distance from vertex 1 to i                                    |
| **orig[i]** | Parent of i (used to rebuild the path)                                 |
| **pq**      | Min-heap (priority queue) that always gives the smallest distance node |
| **INF**     | A very large value (e.g., 1e18)                                        |

---

## 💡 Pseudocode

```
FUNCTION Dijkstra(n, m, edges):
    Initialize graph as adjacency list
    For each edge (a, b, w):
        Add (b, w) to graph[a]
        Add (a, w) to graph[b]

    For i = 1 to n:
        dist[i] = INF
        orig[i] = -1

    dist[1] = 0
    pq = priority_queue()
    pq.push((0, 1)) // (distance, vertex)

    WHILE pq is not empty:
        (d, u) = pq.top()
        pq.pop()

        IF d > dist[u]:
            CONTINUE

        FOR each (v, w) in graph[u]:
            IF dist[u] + w < dist[v]:
                dist[v] = dist[u] + w
                orig[v] = u
                pq.push((dist[v], v))

    IF dist[n] == INF:
        RETURN -1
    ELSE:
        BUILD path from n to 1 using orig[]
        REVERSE path
        PRINT path
```

---

## 🧩 Sample Input

```
5 6
1 2 2
2 5 5
2 3 4
1 4 1
4 3 3
3 5 1
```

---

# 🧱 Step-by-Step Visualization

| Step | Current Node | Neighbors (v, w)    | Relaxation            | Updated dist[]          | PQ Content   |
| ---- | ------------ | ------------------- | --------------------- | ----------------------- | ------------ |
| Init | —            | —                   | —                     | dist[1] = 0, others = ∞ | (0, 1)       |
| 1    | 1            | (2,2), (4,1)        | dist[2]=2, dist[4]=1  | [0,2,∞,1,∞]             | (1,4), (2,2) |
| 2    | 4            | (1,1), (3,3)        | dist[3]=4             | [0,2,4,1,∞]             | (2,2), (4,3) |
| 3    | 2            | (1,2), (5,5), (3,4) | dist[5]=7, dist[3]=4  | [0,2,4,1,7]             | (4,3), (7,5) |
| 4    | 3            | (2,4), (4,3), (5,1) | dist[5]=5 (improved!) | [0,2,4,1,5]             | (5,5)        |
| 5    | 5            | done                | —                     | —                       | —            |

---

## 🔄 Path Reconstruction

Tracing back using **orig[]**:

```
5 ← 3 ← 4 ← 1
```

So the path is:

### ✅ Output Path:

```
1 → 4 → 3 → 5
```

---

# ⏱️ Time Complexity Analysis

| Complexity | Explanation                                                  |
| ---------- | ------------------------------------------------------------ |
| **Time**   | O((n + m) log n) — each edge relaxed at most once + min-heap |
| **Space**  | O(n + m) — adjacency list + dist[] + orig[]                  |

---

# 🧾 Summary

| Topic                 | Explanation                                               |
| --------------------- | --------------------------------------------------------- |
| **Problem**           | Find shortest path from vertex 1 to n in a weighted graph |
| **Algorithm**         | Dijkstra’s Algorithm                                      |
| **Graph Type**        | Undirected, Weighted                                      |
| **Negative weights?** | Not supported                                             |
| **Data Structure**    | Min-heap (priority queue)                                 |
| **Result**            | Shortest path or -1                                       |



