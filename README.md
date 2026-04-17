 🧩 Sudoku Game

A fully playable Sudoku desktop game built in Python with **Tkinter** — featuring procedural puzzle generation, a backtracking solver, hint system, and a live timer. Every puzzle is unique, has exactly one solution, and is generated fresh on each new game.

---

 🎮 Features

- Procedural puzzle generation — every game produces a randomised, unique puzzle guaranteed to have exactly one solution
- Backtracking solver — auto-solves any valid board instantly using recursive depth-first search
- Hint system — reveals one empty cell at a time from the stored solution
- Live timer — counts elapsed seconds from the moment a new game starts
- Win detection — compares the player's board to the precomputed solution on demand
- Visual 3×3 box borders — thicker padding visually separates the nine sub-grids
- Colour-coded cells — original clues in black (disabled), player entries in blue
- Pure Python* — only the standard library; no third-party packages required

---

 🗂️ Project Structure

```
sudoku.py
├── create_board()          # Returns a blank 9×9 board (list of lists)
├── is_valid()              # Checks row, column, and 3×3 box constraints
├── find_empty()            # Scans for the next unfilled cell
├── solve_sudoku()          # Backtracking solver (in-place)
├── count_solutions()       # Confirms uniqueness — stops at 2
├── fill_board()            # Randomised fill using shuffled digits
├── generate_puzzle()       # Full pipeline: fill → deepcopy → remove cells
└── SudokuGUI               # Tkinter controller — board, buttons, timer
    ├── create_grid()       # Builds 81 Entry widgets with box-border padding
    ├── new_game()          # Generates and loads a fresh puzzle
    ├── update_timer()      # Schedules itself every 1000 ms via root.after()
    ├── get_board()         # Reads Entry widgets into a 9×9 list
    ├── solve()             # Fills all cells from self.solution
    ├── give_hint()         # Reveals the first empty cell's solution value
    └── check_win()         # Compares current board to solution
```

---

🧱 Data Structures & Algorithms

| Structure / Algorithm | Where used | Detail |
|---|---|---|
| 2D list `list[list[int]]` | `board`, `puzzle`, `solution`, `original` | 9×9 grid; O(1) cell access by `[row][col]` |
| Recursive backtracking (DFS) | `solve_sudoku()`, `fill_board()`, `count_solutions()` | Explores candidates 1–9, backtracks on conflict |
| Constraint propagation | `is_valid()` | Row + column + box checks before placing a digit |
| `copy.deepcopy()` | `generate_puzzle()` | Preserves the solved board independently of the puzzle copy |
| Random shuffle | `fill_board()` | `random.shuffle(nums)` ensures different puzzles each run |
| Uniqueness guard | `count_solutions()` | Early-exit at count > 1 keeps generation fast |
| `root.after()` scheduler | `update_timer()` | Non-blocking 1 s callback — avoids `time.sleep()` on the main thread |

 Backtracking — how it works

```
find_empty() → try digits 1–9
  └─ is_valid()? → place digit → recurse
       └─ dead end? → board[row][col] = 0 → backtrack
```

`count_solutions()` runs the same algorithm but counts instead of stopping at the first solution. This ensures every generated puzzle has exactly one valid completion before it is shown to the player.

---

 🚀 Getting Started

 Prerequisites

- Python 3.8 or later
- Tkinter (bundled with most Python installations)

> Linux users: if Tkinter is missing, install it with:
> ```bash
> sudo apt install python3-tk
> ```

Run

```bash
python sudoku.py
```

---

 🕹️ How to Play

1. Launch the app — a freshly generated puzzle loads automatically.
2. Click any **blue cell** and type a digit (1–9).
3. Use the buttons at the bottom as needed:

| Button | Action |
|---|---|
| New Game | Generates a brand-new puzzle and resets the timer |
| Hint | Fills in one empty cell with the correct value |
| Solve | Reveals the full solution immediately |
| Check | Tells you whether your current board is correct |

4. Solve all 81 cells correctly and click **Check** to see your finishing time.


 🔧 Customisation

| What to change | Where |
|---|---|
| Puzzle difficulty (more/fewer clues) | Increase or decrease `attempts` in `generate_puzzle()` |
| Font size | `font=("Arial", 20, "bold")` in `create_grid()` |
| Hint colour | `fg` value in `give_hint()` |
| Timer interval | Change `1000` (ms) in `update_timer()` |

---

📄 License

This project is open source and available under the [MIT License](LICENSE).

---

> Built as a Python learning project demonstrating recursive algorithms, constraint satisfaction, GUI programming with Tkinter, and procedural puzzle generation.
