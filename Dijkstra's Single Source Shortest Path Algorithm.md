# Ex. No: 18C - Dijkstra's Single Source Shortest Path Algorithm

## AIM:
To write a Python program for **Dijkstra's single source shortest path algorithm**.

## ALGORITHM:

**Step 1**: Initialize a `distance[]` array with infinity for all vertices except the source, which is set to `0`.  
Create a `sptSet[]` array (shortest path tree set) to keep track of vertices whose shortest distance from the source is finalized.

**Step 2**: Pick the vertex `u` with the minimum distance value from the set of vertices not yet processed.

**Step 3**: For every adjacent vertex `v` of the picked vertex `u`, if the current distance to `v` is greater than the distance to `u` plus the edge weight `(u, v)`, then update the distance of `v`.

**Step 4**: Mark the vertex `u` as processed in `sptSet`.

**Step 5**: Repeat Steps 2–4 until all vertices are processed.

**Step 6**: Print the shortest distances from the source to all other vertices.

## PYTHON PROGRAM

```
# Function to find the vertex with the minimum distance from the set of vertices not yet processed
def min_distance(dist, spt_set, V):
    min_val = float("inf")
    min_index = -1
    
    for v in range(V):
        if dist[v] < min_val and not spt_set[v]:
            min_val = dist[v]
            min_index = v
    return min_index

# Function to implement Dijkstra's algorithm
def dijkstra(graph, src, V):
    dist = [float("inf")] * V  # Initialize distances to infinity
    dist[src] = 0  # Distance to the source is always 0
    spt_set = [False] * V  # Set to track vertices whose shortest path is finalized
    
    for _ in range(V):
        u = min_distance(dist, spt_set, V)  # Pick the vertex with the minimum distance
        spt_set[u] = True  # Mark it as processed
        
        # Update the distance for all adjacent vertices of u
        for v in range(V):
            if not spt_set[v] and graph[u][v] != 0 and dist[u] != float("inf") and dist[u] + graph[u][v] < dist[v]:
                dist[v] = dist[u] + graph[u][v]
    
    # Print the final distances
    print("Vertex \t Distance from Source")
    for i in range(V):
        print(f"{i} \t {dist[i]}")

# Example Graph represented as an adjacency matrix
graph = [
    [0, 10, 0, 0, 0, 0],
    [10, 0, 5, 0, 0, 0],
    [0, 5, 0, 20, 0, 0],
    [0, 0, 20, 0, 10, 0],
    [0, 0, 0, 10, 0, 5],
    [0, 0, 0, 0, 5, 0]
]

V = 6  # Number of vertices
src = 0  # Source vertex

# Calling the Dijkstra function
dijkstra(graph, src, V)


```

## OUTPUT

![image](https://github.com/user-attachments/assets/119adff5-9a74-42b5-ac95-edcfde910d6f)

## RESULT
The program successfully computes and prints the shortest path from the source vertex (vertex 0) to all other vertices in the graph using Dijkstra's algorithm.
