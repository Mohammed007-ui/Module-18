# Ex. No: 18A - Prim's Minimum Spanning Tree (MST) Algorithm

## AIM:
To write a Python program for **Prim's Minimum Spanning Tree (MST)** algorithm.

## ALGORITHM:

**Step 1**: Initialize the `key[]` array to infinity, set the first vertex's key to `0`, and create `mstSet[]` and `parent[]` arrays.

**Step 2**: Select the vertex with the smallest key value not yet included in `mstSet`.

**Step 3**: Add the selected vertex to `mstSet`.

**Step 4**: For all adjacent vertices:
- If the edge weight is smaller than their current key value, and the vertex is not in `mstSet`, then:
  - Update their key value
  - Update their parent to the current vertex

**Step 5**: Repeat Steps 2–4 until all vertices are included in the MST.

**Step 6**: Print the resulting Minimum Spanning Tree using the `parent[]` array.

## PYTHON PROGRAM

```
def minKey(key, mstSet):
    min_val = 10**9  # large number instead of sys.maxsize
    min_index = -1
    for v in range(len(key)):
        if key[v] < min_val and not mstSet[v]:
            min_val = key[v]
            min_index = v
    return min_index

def primMST(graph):
    V = len(graph)
    key = [10**9] * V
    parent = [None] * V
    key[0] = 0
    mstSet = [False] * V

    parent[0] = -1  # First node is root

    for _ in range(V):
        u = minKey(key, mstSet)
        mstSet[u] = True

        for v in range(V):
            if graph[u][v] > 0 and not mstSet[v] and key[v] > graph[u][v]:
                key[v] = graph[u][v]
                parent[v] = u

    print("Edge \tWeight")
    for i in range(1, V):
        print(f"{parent[i]} - {i}\t{graph[i][parent[i]]}")

# Example graph
graph = [
    [0, 2, 0, 6, 0],
    [2, 0, 3, 8, 5],
    [0, 3, 0, 0, 7],
    [6, 8, 0, 0, 9],
    [0, 5, 7, 9, 0]
]

primMST(graph)

```

## OUTPUT

![image](https://github.com/user-attachments/assets/a48ddaee-a7e5-40c2-b273-64ab35ad5592)



## RESULT
The program implements Prim's Minimum Spanning Tree algorithm. It successfully computes and prints the edges included in the MST along with their weights and the total minimum cost of the MST.
