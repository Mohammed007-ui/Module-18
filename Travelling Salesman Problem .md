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
from itertools import permutations

def tsp(distance_matrix):
    n = len(distance_matrix)
    cities = list(range(1, n))  # all cities except starting city 0
    min_cost = float('inf')
    best_route = []

    for perm in permutations(cities):
        current_cost = 0
        k = 0  # start from city 0
        for j in perm:
            current_cost += distance_matrix[k][j]
            k = j
        current_cost += distance_matrix[k][0]  # return to starting city

        if current_cost < min_cost:
            min_cost = current_cost
            best_route = [0] + list(perm) + [0]

    return best_route, min_cost

# Example distance matrix
distance_matrix = [
    [0, 10, 15, 20],
    [10, 0, 35, 25],
    [15, 35, 0, 30],
    [20, 25, 30, 0]
]

route, cost = tsp(distance_matrix)
print("Shortest route:", route)
print("Minimum cost:", cost)

```

## OUTPUT

![image](https://github.com/user-attachments/assets/b63c92df-6f08-4627-b465-b36b1c3f742b)


##RESULT

The program computes all permutations of cities except the starting city, calculates the total travel cost for each route starting and ending at city 0, and outputs the route with the minimum cost. This brute-force solution works well for a small number of cities.








