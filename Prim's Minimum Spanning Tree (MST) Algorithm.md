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
class PrimMST:
    def __init__(self, vertices, graph):
        self.V = vertices  # Number of vertices
        self.graph = graph  # Graph represented as an adjacency matrix

    # Function to find the vertex with the minimum key value
    def min_key(self, key, mstSet):
        min_val = float("inf")
        min_index = -1

        for v in range(self.V):
            if key[v] < min_val and not mstSet[v]:
                min_val = key[v]
                min_index = v
        return min_index

    def prim(self):
        key = [float("inf")] * self.V  # Initialize all key values to infinity
        parent = [-1] * self.V  # Array to store constructed MST
        mstSet = [False] * self.V  # Boolean array to track vertices included in MST

        key[0] = 0  # Starting with vertex 0
        parent[0] = -1  # First node has no parent

        # Find the MST for all vertices
        for _ in range(self.V):
            # Pick the vertex with the minimum key value
            u = self.min_key(key, mstSet)

            # Include the picked vertex in the MST
            mstSet[u] = True

            # Update the key value and parent index of the adjacent vertices of the picked vertex
            for v in range(self.V):
                # Update key and parent if v is not in mstSet and the weight of the edge u-v is less than the current key of v
                if self.graph[u][v] and not mstSet[v] and self.graph[u][v] < key[v]:
                    key[v] = self.graph[u][v]
                    parent[v] = u

        # Print the MST
        self.print_mst(parent)

    def print_mst(self, parent):
        print("Edge \tWeight")
        for i in range(1, self.V):
            print(f"{parent[i]} - {i} \t{self.graph[i][parent[i]]}")


# Example Graph (Adjacency Matrix Representation)
graph = [
    [0, 2, 0, 6, 0],
    [2, 0, 3, 8, 5],
    [0, 3, 0, 0, 7],
    [6, 8, 0, 0, 9],
    [0, 5, 7, 9, 0]
]

# Number of vertices in the graph
V = 5

# Create an object of PrimMST
prim = PrimMST(V, graph)

# Get the MST using Prim's algorithm
prim.prim()

```

## OUTPUT

![image](https://github.com/user-attachments/assets/01aa4018-3c4d-4804-a207-2c6cbcbff0c6)

## RESULT
This is the correct implementation of Prim's algorithm for finding the Minimum Spanning Tree of a connected, undirected graph. The output matches the expected MST, and the total weight is minimized.

