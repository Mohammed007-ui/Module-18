# Ex. No: 18D - Travelling Salesman Problem (TSP)

## AIM:
To write a Python program to find the shortest possible route that visits every city exactly once and returns to the starting point using the **Travelling Salesman Problem (TSP)** approach.

## ALGORITHM:

**Step 1**: Start the program.

**Step 2**: Input the number of cities and the distance matrix.

**Step 3**: Set the starting city (e.g., city `0`).

**Step 4**: Generate all possible permutations of the remaining cities.

**Step 5**: For each permutation:
- Calculate the total cost of traveling through the permutation starting and ending at city `0`.
- Keep track of the **minimum cost** and the corresponding route.

**Step 6**: Return the **route** and the **minimum cost**.

**Step 7**: End the program.

## PYTHON PROGRAM

```
import itertools

def calculate_cost(route, dist_matrix):
    cost = 0
    for i in range(len(route) - 1):
        cost += dist_matrix[route[i]][route[i + 1]]
    cost += dist_matrix[route[-1]][route[0]]  # Return to the starting city
    return cost

def tsp(dist_matrix):
    # Number of cities
    n = len(dist_matrix)
    
    # Generate all possible routes (permutations)
    cities = list(range(1, n))  # List of cities except the starting city (city 0)
    all_routes = itertools.permutations(cities)

    min_cost = float("inf")
    best_route = None

    # Evaluate each route
    for route in all_routes:
        # Add starting city to the route
        full_route = [0] + list(route)
        cost = calculate_cost(full_route, dist_matrix)
        
        if cost < min_cost:
            min_cost = cost
            best_route = full_route

    return best_route, min_cost

# Example: Distance matrix for 4 cities (0, 1, 2, 3)
dist_matrix = [
    [0, 10, 15, 20],
    [10, 0, 35, 25],
    [15, 35, 0, 30],
    [20, 25, 30, 0]
]

# Call the TSP function
best_route, min_cost = tsp(dist_matrix)

# Print the result
print("Best route:", best_route)
print("Minimum cost:", min_cost)


```

## OUTPUT

![image](https://github.com/user-attachments/assets/49996e3e-64aa-41b8-af5f-3d6b5e14fcdc)


##RESULT
The algorithm correctly computes the best route and the minimum cost for the Travelling Salesman Problem using brute force permutation generation. This approach works for small numbers of cities but may not be efficient for large-scale problems due to its factorial time complexity (O(n!)).
