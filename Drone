import numpy as np
import matplotlib.pyplot as plt
import time

# -----------------------
# Environment Setup
# -----------------------
GRID_SIZE = (20, 20)
OBSTACLE_DENSITY = 0.2

def generate_grid(size, obstacle_density):
    grid = np.zeros(size)
    obstacles = np.random.rand(*size) < obstacle_density
    grid[obstacles] = 1  # 1 = obstacle
    return grid

grid = generate_grid(GRID_SIZE, OBSTACLE_DENSITY)

start = (0, 0)
if grid[start] == 1:
    grid[start] = 0  # ensure start is free

# -----------------------
# Sequential Coverage (Lawnmower Pattern)
# -----------------------
def sequential_coverage(grid, start):
    rows, cols = grid.shape
    path = []
    visited = np.zeros_like(grid)
    x, y = start

    for i in range(rows):
        if i % 2 == 0:  # move left to right
            for j in range(cols):
                if grid[i, j] == 0:
                    path.append((i, j))
                    visited[i, j] = 1
        else:  # move right to left
            for j in range(cols-1, -1, -1):
                if grid[i, j] == 0:
                    path.append((i, j))
                    visited[i, j] = 1
    return path, visited

# -----------------------
# Run Simulation
# -----------------------
path, visited = sequential_coverage(grid, start)

plt.ion()
fig, ax = plt.subplots(figsize=(6, 6))
ax.set_title("Autonomous Drone Sequential Coverage (Lawnmower Path)")
ax.imshow(grid, cmap='gray_r')

drone_dot, = ax.plot([], [], 'bo', markersize=6)
visited_map = np.copy(grid)

for pos in path:
    visited_map[pos] = 0.5
    drone_dot.set_data([pos[1]], [pos[0]])  # ✅ pass as list
    ax.imshow(visited_map, cmap='gray_r')
    plt.pause(0.05)

plt.ioff()
plt.show()

covered_cells = np.sum(visited)
total_free = np.sum(grid == 0)
print(f"Sequential coverage complete: {covered_cells}/{total_free} free cells visited ({covered_cells/total_free:.1%})")
