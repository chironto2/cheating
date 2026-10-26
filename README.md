# Computer Graphics: Circle Drawing Algorithms

This repository implements two fundamental rasterization algorithms for drawing circles in 2D computer graphics:
1. **Bresenham's Circle Drawing Algorithm**
2. **Midpoint Circle Drawing Algorithm**

---

## 📖 Algorithm Overview & Formulations

### 1. Bresenham's Circle Drawing Algorithm
Uses integer calculations to determine pixel selections in the first octant ($x = 0$ to $x = y$).

* **Initial Decision Parameter:**  
  $$d_0 = 3 - 2r$$
* **Update Rules:**
  * If $d_k < 0$:  
    $$d_{k+1} = d_k + 4x_k + 6$$  
    $$x_{k+1} = x_k + 1, \quad y_{k+1} = y_k$$
  * If $d_k \ge 0$:  
    $$d_{k+1} = d_k + 4(x_k - y_k) + 10$$  
    $$x_{k+1} = x_k + 1, \quad y_{k+1} = y_k - 1$$

---

### 2. Midpoint Circle Drawing Algorithm
Evaluates the implicit circle function $f(x, y) = x^2 + y^2 - r^2$ at the midpoint between candidate pixels.

* **Initial Decision Parameter:**  
  $$p_0 = 1 - r$$
* **Update Rules:**
  * If $p_k < 0$:  
    $$p_{k+1} = p_k + 2x_{k+1} + 1$$  
    $$x_{k+1} = x_k + 1, \quad y_{k+1} = y_k$$
  * If $p_k \ge 0$:  
    $$p_{k+1} = p_k + 2x_{k+1} + 1 - 2y_{k+1}$$  
    $$x_{k+1} = x_k + 1, \quad y_{k+1} = y_k - 1$$

---

## 🛠 Explanation of Built-in Functions & Methods

| Function / Method | Usage in Code | Description |
| :--- | :--- | :--- |
| `append()` | `first_octant_pixels.append((x, y))` | Adds a new tuple/item to the end of a list. |
| `extend()` | `pixels.extend([...])` | Adds all elements from an iterable (list) to the end of the existing list. |
| `add()` | `all_pixels.add(pt)` | Inserts a unique element into a Python `set`. Automatically eliminates duplicate coordinates. |
| `sorted()` | `sorted(list(all_pixels))` | Returns a new ordered list from the elements of any iterable. |
| `reversed()` | `reversed(first_octant)` | Returns a reverse iterator over the list to maintain continuous perimeter ordering. |
| `int()` | `int(input(...))` | Converts user input strings into integers. |
| `input()` | `input("Enter center coordinate xc: ")` | Reads a string line from standard user input. |

---

## 📊 Explanation of Matplotlib Visualization Methods

| Function / Method | Description |
| :--- | :--- |
| `plt.figure(figsize=(w, h))` | Creates a new figure with specified width and height dimensions. |
| `plt.scatter(x, y)` | Plots discrete pixel coordinates as individual points. |
| `plt.plot(x, y, marker='o')` | Plots pixel points and connects them sequentially with line segments. |
| `plt.Circle((xc, yc), r)` | Creates a true continuous reference circle patch object. |
| `plt.gca().add_patch(...)` | Adds a graphical patch (like the reference circle) to the current axes object. |
| `plt.gca().set_aspect('equal')` | Enforces equal $1:1$ scaling between X and Y axes so circles appear round instead of stretched ovals. |
| `plt.grid(True)` | Displays grid lines on the coordinate system for clear pixel alignment visibility. |
| `plt.title()`, `plt.xlabel()`, `plt.ylabel()` | Sets graph labels and header titles. |
| `plt.show()` | Displays the plotted figure in the window or notebook output. |

---

## 🔄 8-Way Symmetry Concept

Circle equations possess 8-fold symmetry. Calculating pixels for one octant ($0^\circ$ to $45^\circ$) allows plotting all 8 octants simultaneously using offset transformations:

$$(xc \pm x, yc \pm y) \quad \text{and} \quad (xc \pm y, yc \pm x)$$