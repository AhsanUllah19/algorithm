# 🌟 Bicoloring (BFS) Problem Analysis
## 🧩 Problem: Graph Bicoloring

Can a graph be colored using only two colors?
We need to determine whether a graph can be colored using exactly two colors (e.g., white and black) such that **no two adjacent nodes share the same color**.



## 🧠 Key Concept: Bipartite Graph

If a graph can be colored using two colors without any adjacent nodes having the same color, then the graph is called a **Bipartite Graph**.

A bipartite graph’s nodes can be divided into two **disjoint sets**:

* **Set A**
* **Set B**

Every edge must connect a node from **Set A** to **Set B**, and vice versa.


## 🚫 When is Bicoloring NOT Possible?

### Condition

If a graph contains an **Odd-Length Cycle**, then it **cannot** be bicolored.

### Example

A triangle (3-cycle) cannot be bicolored:

* If the first node is colored with one color,
* The second gets the opposite color,
* The third gets the same color as the first node,
  But the third node is also adjacent to the first node — causing a **color conflict**.
  This means the graph is **not bicolorable**.

---

## 🔍 Solution Algorithm: Breadth-First Search (BFS)

We use the BFS traversal algorithm to check if a graph is bicolorable.
During BFS, we assign colors (0 and 1) alternately to nodes and check whether adjacent nodes receive the same color.

---

## 🛠️ Steps of the Algorithm

1️⃣ **Initialization:**
Mark all nodes as **Uncolored (-1)**.

2️⃣ **Start BFS:**
Begin BFS from node 0 using a queue.
Assign color **0** to this node.

3️⃣ **Traversal:**
Pop a node **u** from the queue.
For each of its neighbors **v**, try to assign the opposite color:
**color[v] = 1 - color[u]**

4️⃣ **Conflict Check:**
If a neighbor **v** is already colored **and**
`color[v] == color[u]`,
then an **Odd Cycle** exists, and the graph is **NOT BICOLORABLE**.

5️⃣ **Completion:**
If BFS completes without any conflict, the graph is **BICOLORABLE**.

---

## 💻 Pseudocode

```
function isBicolorable(graph):
    n = total number of nodes
    color = array of size n, initialize with -1

    for each node i in graph:
        if color[i] == -1:
            color[i] = 0
            queue.push(i)

            while queue not empty:
                u = queue.pop()

                for each v in graph[u]:
                    if color[v] == -1:
                        color[v] = 1 - color[u]
                        queue.push(v)
                    else if color[v] == color[u]:
                        return "NOT BICOLORABLE"

    return "BICOLORABLE"


