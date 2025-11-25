## ♞ Knight Moves (BFS in a 2D Grid) — Shortest Path for a Knight

### 🔍 What is the problem?

The task is to solve a classic **shortest-path** problem.

Given two squares **a** and **b** on a chessboard, the goal is to determine
**the minimum number of moves a knight needs to go from a to b**.

We can model this as a shortest-path problem on an **unweighted graph**.

## 🎯 Modeling the Problem

| Concept   | Meaning                                 |
| --------- | --------------------------------------- |
| **Nodes** | The 64 squares of the chessboard        |
| **Edges** | A valid knight move between two squares |
| **Cost**  | Each move costs the same (1 step)       |

Since the graph is unweighted, the ideal algorithm for finding the shortest path is **Breadth-First Search (BFS)**.

---

## 🧠 What is BFS?

**BFS (Breadth-First Search)** is a graph-traversal algorithm that starts from a source node and explores the graph **level by level** based on distance.

It uses a **queue** data structure and guarantees that it will always find the shortest path first before going through any longer path.

In unweighted graphs (like our knight-move graph), BFS is the **most efficient** way to compute shortest paths.

---

## 🎲 Representing the Board and Knight's Moves

Before using BFS, we must represent the graph in code — specifically, how a knight moves from one square to another.

---

## ♘ Knight’s 8 Possible Moves

From a position **(i, j)**, a knight can move to 8 possible squares:

* (i−2, j+1)
* (i−2, j−1)
* (i−1, j+2)
* (i−1, j−2)
* (i+1, j+2)
* (i+1, j−2)
* (i+2, j+1)
* (i+2, j−1)

---

## 💻 Converting into Code

```cpp
// kr[] stores the row offsets for the 8 knight moves
const int kr[] = {2, 2, -2, -2, 1, 1, -1, -1};

// kc[] stores the column offsets for the 8 knight moves
const int kc[] = {1, -1, 1, -1, 2, -2, 2, -2};
```

Looping `i = 0` to `7`, we compute:

```
new_r = r + kr[i]
new_c = c + kc[i]
```

This gives all 8 possible new squares from position `(r, c)`.

---

## ⚙️ Using Breadth-First Search (BFS)

BFS is ideal for this problem because it explores the graph in **layers**:

* **Layer 0** – starting square (distance 0)
* **Layer 1** – squares reachable in 1 move
* **Layer 2** – squares reachable in 2 moves
* … and so on.

The first time BFS reaches the target square, we are guaranteed that
**this is the shortest possible path**.

---

## 🧩 Required Arrays

| Name                     | Purpose                                                     |
| ------------------------ | ----------------------------------------------------------- |
| `dist[8][8]`             | Stores the minimum number of moves from the starting square |
| `color[8][8]`            | Tracks the visitation state of each square                  |
| `queue<pair<int,int>> q` | Stores squares to be visited next                           |

---

## 🎨 Meaning of `color` Values

* **-1 → White** (not visited)
* **1 → Gray** (in queue, currently being explored)
* **2 → Black** (fully processed)


