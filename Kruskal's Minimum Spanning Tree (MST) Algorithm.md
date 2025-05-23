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
# Kruskal's Minimum Spanning Tree (MST) Algorithm

class Graph:
    def __init__(self, vertices):
        self.V = vertices
        self.edges = []  # list to store all edges in format (weight, u, v)

    def add_edge(self, u, v, w):
        self.edges.append((w, u, v))

    # Find set of an element i (uses path compression technique)
    def find(self, parent, i):
        if parent[i] != i:
            parent[i] = self.find(parent, parent[i])
        return parent[i]

    # Union of two sets x and y (uses union by rank)
    def union(self, parent, rank, x, y):
        xroot = self.find(parent, x)
        yroot = self.find(parent, y)

        if rank[xroot] < rank[yroot]:
            parent[xroot] = yroot
        elif rank[xroot] > rank[yroot]:
            parent[yroot] = xroot
        else:
            parent[yroot] = xroot
            rank[xroot] += 1

    def kruskal_mst(self):
        result = []  # store the resultant MST edges

        # Step 1: Sort all edges in non-decreasing order by weight
        self.edges = sorted(self.edges, key=lambda item: item[0])

        parent = []
        rank = []

        # Create V subsets with single elements
        for node in range(self.V):
            parent.append(node)
            rank.append(0)

        e = 0  # count of edges in MST
        i = 0  # index variable for sorted edges

        while e < self.V - 1 and i < len(self.edges):
            w, u, v = self.edges[i]
            i += 1

            x = self.find(parent, u)
            y = self.find(parent, v)

            # If including this edge doesn't cause cycle, include it in result
            if x != y:
                e += 1
                result.append((u, v, w))
                self.union(parent, rank, x, y)

        # Print the constructed MST
        print("Edges in the Minimum Spanning Tree:")
        total_weight = 0
        for u, v, weight in result:
            print(f"{u} -- {v} == {weight}")
            total_weight += weight
        print(f"Total minimum cost: {total_weight}")

# Example usage:

g = Graph(4)
g.add_edge(0, 1, 10)
g.add_edge(0, 2, 6)
g.add_edge(0, 3, 5)
g.add_edge(1, 3, 15)
g.add_edge(2, 3, 4)

g.kruskal_mst()

```

## OUTPUT

![image](https://github.com/user-attachments/assets/d066a6de-64b0-453d-a0c2-f33731f41127)


## RESULT
The program successfully finds the Minimum Spanning Tree of the given weighted graph using Kruskal's algorithm, printing the edges included in the MST and the total minimum cost.
