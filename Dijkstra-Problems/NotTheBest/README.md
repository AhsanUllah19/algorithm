# 🚦 Second Shortest Path (Modified Dijkstra Algorithm)

Robin lives in a village with **N intersections** and **R bidirectional roads**.
He wants to travel from **1 → N**, but instead of the shortest path,
he wants the **second-shortest path**.

---

# 🧠 Problem Definition

A **second-shortest path** means:

* It is **strictly longer** than the shortest path
* But **shorter than all other possible longer paths**
* Edges **may be reused**
* All weights are **positive**

For each test case, you must print:

```
Case X: second_shortest_path_cost
```

---

# 🔍 Algorithm Overview — Modified Dijkstra

For each node **v**, we maintain **two distances**:

* **dist1[v]** → the shortest distance to v
* **dist2[v]** → the second-shortest distance to v

## Relaxation Rules

### 1️⃣ If the new path is **shorter than dist1[v]**:

* The new path becomes **dist1[v]**
* The old **dist1[v]** becomes **dist2[v]**

### 2️⃣ Else if:

```
dist1[v] < new_path < dist2[v]
```

Update **dist2[v] = new_path**

A priority queue (min-heap) ensures:

* The smallest current distance is always processed first
* dist1 and dist2 remain correctly updated

---

# 📌 Input Format

```
T
N R
u v w
u v w
...
```

Where:

| Symbol | Meaning                          |
| ------ | -------------------------------- |
| **T**  | Number of test cases             |
| **N**  | Number of intersections (1–5000) |
| **R**  | Number of roads (1–100000)       |
| **w**  | Weight (1–5000)                  |

---

# 📌 Output Format

```
Case X: result
```

---

# 🧪 Example

### Input

```
2
3 3
1 2 100
2 3 200
1 3 50
4 4
1 2 100
2 4 200
2 3 250
3 4 100
```

### Output

```
Case 1: 150
Case 2: 450
```

---

# 🛠️ How to Compile

```
g++ -std=c++17 second_shortest.cpp -o second
```

---

# Step-By-Step Solution

### Second Shortest Path Example

We use the following single test case:

```
1
4 4
1 2 100
2 4 200
2 3 250
3 4 100
```

Goal: **Find the second-shortest path from 1 → 4**

---

# Graph (ASCII)

```
(1)---100---(2)---200---(4)
              |
             250
              |
             (3)---100---(4)
```

Edges:

* 1 → 2 = 100
* 2 → 4 = 200
* 2 → 3 = 250
* 3 → 4 = 100

---

# Initial State

```
dist1 = [inf, 0, inf, inf, inf]  // 1-based indexing
dist2 = [inf, inf, inf, inf, inf]
PQ = {(0,1)}
```

---

# Step-by-Step Execution

---

## **Step 1 — Pop (0,1)**

Relax neighbors of node 1:

* 1 → 2: new_dist = 100 → update dist1[2] = 100

Push (100,2)

### State:

```
dist1 = [inf, 0, 100, inf, inf]
dist2 = [inf, inf, inf, inf, inf]
PQ = {(100,2)}
```

---

## **Step 2 — Pop (100,2)**

Relax:

* 2 → 1 : new_dist = 200 → update dist2[1] = 200
* 2 → 4 : new_dist = 300 → dist1[4] = 300
* 2 → 3 : new_dist = 350 → dist1[3] = 350

### State:

```
dist1 = [inf, 0, 100, 350, 300]
dist2 = [inf, 200, inf, inf, inf]
PQ = {(200,1), (300,4), (350,3)}
```

---

## **Step 3 — Pop (200,1)**

Relax:

* 1 → 2 : new_dist = 300 → update dist2[2] = 300

### State:

```
dist1 = [inf, 0, 100, 350, 300]
dist2 = [inf, 200, 300, inf, inf]
PQ = {(300,2), (300,4), (350,3)}
```

---

## **Step 4 — Pop (300,2)**

Relax:

* 2 → 4 : new_dist = 500 → dist2[4] = 500
* 2 → 3 : new_dist = 550 → dist2[3] = 550

### State:

```
dist1 = [inf, 0, 100, 350, 300]
dist2 = [inf, 200, 300, 550, 500]
PQ = {(300,4), (350,3), (500,4), (550,3)}
```

---

## **Step 5 — Pop (300,4)**

Relax:

* 4 → 3 : new_dist = 400 → dist2[3] = 400

### State:

```
dist1 = [inf, 0, 100, 350, 300]
dist2 = [inf, 200, 300, 400, 500]
PQ = {(350,3), (400,3), (500,4), (550,3)}
```

---

## **Step 6 — Pop (350,3)**

Relax:

* 3 → 4 : new_dist = 450 → update dist2[4] = 450

### State:

```
dist1 = [inf, 0, 100, 350, 300]
dist2 = [inf, 200, 300, 400, 450]
PQ = {(400,3), (450,4), (500,4), (550,3)}
```

After this, no further updates occur.
→ **dist2[4] = 450 is final**

---

# 🎯 Final Result

| Type                | Path          | Cost    |
| ------------------- | ------------- | ------- |
| **Shortest**        | 1 → 2 → 4     | **300** |
| **Second-shortest** | 1 → 2 → 3 → 4 | **450** |

---

# 📎 Conclusion

* The algorithm correctly updates **dist1** and **dist2** arrays
* Priority queue processes nodes by increasing distance
* After all relaxations, **dist2[N]** gives the **second-shortest path cost**

