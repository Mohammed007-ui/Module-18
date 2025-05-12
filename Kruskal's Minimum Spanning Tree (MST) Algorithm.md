# Ex. No: 18B - Kruskal's Minimum Spanning Tree (MST) Algorithm

## AIM:
To write a Python program for **Kruskal's algorithm** to find the Minimum Spanning Tree (MST) of a given connected, undirected, and weighted graph.

## ALGORITHM:

**Step 1**: Sort all the edges of the graph in non-decreasing order of their weights.

**Step 2**: Initialize the `parent[]` and `rank[]` arrays for each vertex to keep track of the disjoint sets.

**Step 3**: Iterate through the sorted edges and pick the smallest edge. Check whether including this edge will form a cycle using the union-find method:
- If the vertices of the edge belong to different sets, include it in the MST.
- Perform a union of these two sets.

**Step 4**: Repeat Step 3 until the MST contains exactly `V-1` edges.

**Step 5**: Print the edges included in the MST and the total minimum cost.

## PYTHON PROGRAM

```
class DisjointSet:
    def __init__(self, n):
        self.parent = [i for i in range(n)]
        self.rank = [0] * n

    # Find the root of the set that contains 'i'
    def find(self, i):
        if self.parent[i] != i:
            self.parent[i] = self.find(self.parent[i])  # Path compression
        return self.parent[i]

    # Union of two subsets
    def union(self, x, y):
        xroot = self.find(x)
        yroot = self.find(y)

        if xroot != yroot:
            # Union by rank
            if self.rank[xroot] < self.rank[yroot]:
                self.parent[xroot] = yroot
            elif self.rank[xroot] > self.rank[yroot]:
                self.parent[yroot] = xroot
            else:
                self.parent[yroot] = xroot
                self.rank[xroot] += 1

class KruskalMST:
    def __init__(self, vertices, edges):
        self.V = vertices  # Number of vertices
        self.edges = edges  # List of edges (weight, u, v)
    
    def kruskal(self):
        mst = []  # To store the final MST
        total_cost = 0
        
        # Step 1: Sort edges in non-decreasing order of their weights
        self.edges.sort(key=lambda x: x[0])

        # Step 2: Initialize DisjointSet
        disjoint_set = DisjointSet(self.V)
        
        # Step 3: Iterate through edges
        for weight, u, v in self.edges:
            # Check if including this edge would form a cycle
            if disjoint_set.find(u) != disjoint_set.find(v):
                # Add edge to the MST
                mst.append((u, v, weight))
                total_cost += weight
                # Perform the union operation
                disjoint_set.union(u, v)

        return mst, total_cost

# Example of a graph represented as (weight, u, v)
edges = [
    (10, 0, 1),
    (20, 0, 2),
    (30, 1, 2),
    (40, 1, 3),
    (50, 2, 3),
    (60, 3, 4)
]

# Number of vertices in the graph
V = 5

# Create an object of KruskalMST
kruskal = KruskalMST(V, edges)

# Get the MST and the total cost
mst, total_cost = kruskal.kruskal()

# Print the MST and its total cost
print("Edges in the Minimum Spanning Tree (MST):")
for u, v, weight in mst:
    print(f"{u} - {v} (Weight: {weight})")

print(f"\nTotal cost of the MST: {total_cost}")

```

## OUTPUT

![image](https://github.com/user-attachments/assets/673bd7ec-bc7d-4fb5-8ebb-cce70cd72ca7)



## RESULT

This is a correct implementation of Kruskal's algorithm to compute the Minimum Spanning Tree for a given graph. The result matches the expected MST and its cost.








