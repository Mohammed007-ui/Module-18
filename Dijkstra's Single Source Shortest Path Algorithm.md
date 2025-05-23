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
def min_distance(dist, sptSet):
    min_val = float('inf')
    min_index = -1
    for v in range(len(dist)):
        if dist[v] < min_val and not sptSet[v]:
            min_val = dist[v]
            min_index = v
    return min_index

def dijkstra(graph, src):
    V = len(graph)
    dist = [float('inf')] * V
    dist[src] = 0
    sptSet = [False] * V

    for _ in range(V):
        u = min_distance(dist, sptSet)
        sptSet[u] = True

        for v in range(V):
            if graph[u][v] > 0 and not sptSet[v] and dist[u] + graph[u][v] < dist[v]:
                dist[v] = dist[u] + graph[u][v]

    print("Vertex \t Distance from Source")
    for i in range(V):
        print(f"{i}\t\t{dist[i]}")

# Example graph (same as before)
graph = [
    [0, 4, 0, 0, 0, 0, 0, 8, 0],
    [4, 0, 8, 0, 0, 0, 0, 11, 0],
    [0, 8, 0, 7, 0, 4, 0, 0, 2],
    [0, 0, 7, 0, 9, 14, 0, 0, 0],
    [0, 0, 0, 9, 0, 10, 0, 0, 0],
    [0, 0, 4, 14, 10, 0, 2, 0, 0],
    [0, 0, 0, 0, 0, 2, 0, 1, 6],
    [8, 11, 0, 0, 0, 0, 1, 0, 7],
    [0, 0, 2, 0, 0, 0, 6, 7, 0]
]

source_vertex = 0
dijkstra(graph, source_vertex)

```

## OUTPUT

![image](https://github.com/user-attachments/assets/7f70ae08-0169-4cef-ac73-18e7cc7c5933)


## RESULT
The program implements Dijkstra's algorithm to compute the shortest path from the source vertex (0) to all other vertices in the graph, correctly printing the minimum distances.
