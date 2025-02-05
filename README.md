# A* Pathfinding Algorithm Visualization

This project is a Python implementation of the A* pathfinding algorithm, visualized using the `pygame` library. The program allows users to interactively set start and end points, draw barriers, and visualize the pathfinding process in real-time.

## Table of Contents
1. [Introduction](#introduction)
2. [Features](#features)
3. [Requirements](#requirements)
4. [Installation](#installation)
5. [Usage](#usage)
6. [Code Explanation](#code-explanation)

---

## Introduction

The A* algorithm is a popular pathfinding algorithm used to find the shortest path between two points in a grid. This project provides an interactive visualization of the A* algorithm, allowing users to create custom grids, set obstacles, and observe how the algorithm navigates from the start to the end point.

---

## Features

- **Interactive Grid**: Users can click to set the start and end points, as well as draw barriers.
- **Real-Time Visualization**: Watch the algorithm explore the grid and find the shortest path in real-time.
- **Customizable Grid Size**: The grid size can be adjusted to create more complex or simpler mazes.
- **Reset Functionality**: Clear the grid and start over with a new configuration.

---

## Requirements

- Python 3.x
- Pygame library

---

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/a-star-pathfinding.git
   cd a-star-pathfinding
   ```

2. Install the required dependencies:
   ```bash
   pip install pygame
   ```

---

## Usage

1. Run the script:
   ```bash
   python a_star_pathfinding.py
   ```

2. Use the mouse to interact with the grid:
   - **Left Click**:
     - Set the **start point** (orange).
     - Set the **end point** (turquoise).
     - Draw **barriers** (black).
   - **Right Click**: Remove start, end, or barriers.

3. Use the keyboard to control the simulation:
   - **Space**: Start the A* algorithm to find the path.
   - **C**: Clear the grid and reset.

---

## Code Explanation

### Key Components

1. **Spot Class**:
   - Represents each cell in the grid.
   - Manages the state of the cell (start, end, barrier, path, etc.).
   - Contains methods to update neighbors and draw the cell on the grid.

   ```python
   class Spot:
       def __init__(self, row, col, width, total_rows):
           self.row = row
           self.col = col
           self.x = row * width
           self.y = col * width
           self.color = WHITE
           self.neighbors = []
           self.width = width
           self.total_rows = total_rows
   ```

2. **A* Algorithm**:
   - Uses a priority queue to explore the grid.
   - Calculates the `g_score` (cost from start) and `f_score` (estimated total cost).
   - Reconstructs the shortest path once the end point is reached.

   ```python
   def algorithm(draw, grid, start, end):
       count = 0
       open_set = PriorityQueue()
       open_set.put((0, count, start))
       came_from = {}
       g_score = {spot: float("inf") for row in grid for spot in row}
       g_score[start] = 0
       f_score = {spot: float("inf") for row in grid for spot in row}
       f_score[start] = h(start.get_pos(), end.get_pos())
   ```

3. **Grid and Visualization**:
   - The grid is created using the `make_grid` function.
   - The `draw` function updates the display with the current state of the grid.

   ```python
   def make_grid(rows, width):
       grid = []
       gap = width // rows
       for i in range(rows):
           grid.append([])
           for j in range(rows):
               spot = Spot(i, j, gap, rows)
               grid[i].append(spot)
       return grid
   ```

4. **User Interaction**
   - The `main` function handles user input (mouse clicks, keyboard presses) and updates the grid accordingly.

   ```python
   def main(win, width):
       ROWS = 50
       grid = make_grid(ROWS, width)
       start = None
       end = None
       run = True
   ```

---
