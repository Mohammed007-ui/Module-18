# Ex. No: 18E - Count the Number of Triangles in an Undirected Graph

## AIM:
To write a Python program to **count the number of triangles** present in an **undirected graph** using matrix operations.

## ALGORITHM:

**Step 1**: Initialize a matrix `aux2` to store the square of the adjacency matrix (i.e., `graph²`).  
Also, initialize a matrix `aux3` to store the cube of the adjacency matrix (i.e., `graph³`).

**Step 2**: Multiply the adjacency matrix with itself to compute `aux2 = graph × graph`.

**Step 3**: Multiply `aux2` with the adjacency matrix again to compute `aux3 = aux2 × graph`.

**Step 4**: Compute the **trace** of the matrix `aux3` (i.e., the sum of diagonal elements of the matrix).

**Step 5**: Divide the trace by **6** to get the number of triangles in the graph.  
*(Each triangle is counted six times in the trace — twice per vertex and once per direction.)*

**Step 6**: Return the result.

## PYTHON PROGRAM

```
import numpy as np

# Function to compute the number of triangles
def count_triangles(graph):
    # Convert the graph into an adjacency matrix
    adj_matrix = np.array(graph)

    # Step 1: Compute graph² (aux2) = graph * graph
    aux2 = np.dot(adj_matrix, adj_matrix)

    # Step 2: Compute graph³ (aux3) = aux2 * graph
    aux3 = np.dot(aux2, adj_matrix)

    # Step 3: Compute the trace of graph³ (sum of diagonal elements)
    trace_aux3 = np.trace(aux3)

    # Step 4: Divide the trace by 6 to get the number of triangles
    # Since each triangle is counted 6 times, once for each of its 3 vertices and each direction
    num_triangles = trace_aux3 // 6

    return num_triangles

# Driver code
def main():
    # Example graph represented by an adjacency matrix
    # For an undirected graph, the matrix is symmetric (i.e., graph[i][j] == graph[j][i])
    graph = [
        [0, 1, 1, 0, 0],
        [1, 0, 1, 1, 0],
        [1, 1, 0, 1, 1],
        [0, 1, 1, 0, 1],
        [0, 0, 1, 1, 0]
    ]
    
    # Count the number of triangles
    triangles = count_triangles(graph)
    print(f"Number of triangles in the graph: {triangles}")

# Run the program
main()

```

## OUTPUT

![image](https://github.com/user-attachments/assets/d83f091b-ea18-4756-adbe-c1d9a5374e8f)


## RESULT
The program calculates the number of triangles using matrix operations and the Havel-Hakimi algorithm, and the result is 2 triangles.
