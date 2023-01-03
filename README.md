# AI_Project_Sudoku

A sudoku solver for Intro to AI course project.

## Overview

### `src` folder
`src` folder contains different modules, all written in Python. 

`solver.py` module contains functions that allow you input a sudoku puzzle then solve it using different methods.

`display.py` module is a utility module that helps you to display the puzzle and the solution. This module relies on the `matplotlib` library.

`collectdata.py` module contains functions that solve all the puzzles in a dataset, record the time taken to solve the puzzles and store them in a `.csv` file.

`sudoku.ipynb` is created from a colab notebook which was used for CNN's approach. 

### `dataset` folder

Contains the datasets used to test run the program.

### `collected_data` folder

Contains all the data collected by the program.

## Usage

First create a new python script in the same directory as the modules.

### The `solver` module

To use, import the module.

```python
import solver
```

The solver use three different algorithms to solve sudoku puzzles
+ Backtracking
+ Simulated Annealing
+ Constraint Propagation

The sudoku puzzle is stored in a 2D list. You can input it by hand,

```python
grid = [[3, 0, 6, 5, 0, 8, 4, 0, 0],
        [5, 2, 0, 0, 0, 0, 0, 0, 0],
        [0, 8, 7, 0, 0, 0, 0, 3, 1],
        [0, 0, 3, 0, 1, 0, 0, 8, 0],
        [9, 0, 0, 8, 6, 3, 0, 0, 5],
        [0, 5, 0, 0, 9, 0, 6, 0, 0],
        [1, 3, 0, 0, 0, 0, 2, 5, 0],
        [0, 0, 0, 0, 0, 0, 0, 7, 4],
        [0, 0, 5, 2, 0, 6, 3, 0, 0]]
```
here empty squares in the puzzle are assigned the value `0`.

Another way is to use the `inputSudoku` function. The function takes in a string representation of the puzzle and returns a 2D list. 

```python
grid = solver.inputSudoku('306508400520000000087000031003010080900863005050090600130000250000000074005206300')
```

`solveBacktracking` solves using backtracking.

```python
sol = solver.solveBacktracking(grid=grid)
```

`solveConstraintPropagation` solves using constraint propagation.

```python
sol = solver.solveConstraintPropagation(grid=grid)
```

`solveSimulatedAnnealing` solves using simulated annealing.

```python
sol = solver.solveSimulatedAnnealing(grid=grid)
```

The `solveSimulatedAnnealing` function has two optional parameters `temp` and `alpha`. These are the starting temperature and the cooling rate of the simulated annealing algorithm, default values are `temp=0.5` and `alpha=0.99999`.

All solver functions return the 2D list representation of the solution.

There is a ultility function to print the sudoku board from the 2D list.

```python
solver.printGrid(grid=grid)
```

An example program:

```python
import solver

grid = solver.inputSudoku('306508400520000000087000031003010080900863005050090600130000250000000074005206300')
sol = solver.solveBacktracking(grid=grid)

print('Puzzle:')
solver.printGrid(grid)
print('Solution:')
solver.printGrid(sol)
```

Output:
```
Puzzle:
╔═══╤═══╤═══╦═══╤═══╤═══╦═══╤═══╤═══╗
║ 3 │   │ 6 ║ 5 │   │ 8 ║ 4 │   │   ║
╟───┼───┼───╫───┼───┼───╫───┼───┼───╢
║ 5 │ 2 │   ║   │   │   ║   │   │   ║
╟───┼───┼───╫───┼───┼───╫───┼───┼───╢
║   │ 8 │ 7 ║   │   │   ║   │ 3 │ 1 ║
╠═══╪═══╪═══╬═══╪═══╪═══╬═══╪═══╪═══╣
║   │   │ 3 ║   │ 1 │   ║   │ 8 │   ║
╟───┼───┼───╫───┼───┼───╫───┼───┼───╢
║ 9 │   │   ║ 8 │ 6 │ 3 ║   │   │ 5 ║
╟───┼───┼───╫───┼───┼───╫───┼───┼───╢
║   │ 5 │   ║   │ 9 │   ║ 6 │   │   ║
╠═══╪═══╪═══╬═══╪═══╪═══╬═══╪═══╪═══╣
║ 1 │ 3 │   ║   │   │   ║ 2 │ 5 │   ║
╟───┼───┼───╫───┼───┼───╫───┼───┼───╢
║   │   │   ║   │   │   ║   │ 7 │ 4 ║
╟───┼───┼───╫───┼───┼───╫───┼───┼───╢
║   │   │ 5 ║ 2 │   │ 6 ║ 3 │   │   ║
╚═══╧═══╧═══╩═══╧═══╧═══╩═══╧═══╧═══╝
Solution:
╔═══╤═══╤═══╦═══╤═══╤═══╦═══╤═══╤═══╗
║ 3 │ 1 │ 6 ║ 5 │ 7 │ 8 ║ 4 │ 9 │ 2 ║
╟───┼───┼───╫───┼───┼───╫───┼───┼───╢
║ 5 │ 2 │ 9 ║ 1 │ 3 │ 4 ║ 7 │ 6 │ 8 ║
╟───┼───┼───╫───┼───┼───╫───┼───┼───╢
║ 4 │ 8 │ 7 ║ 6 │ 2 │ 9 ║ 5 │ 3 │ 1 ║
╠═══╪═══╪═══╬═══╪═══╪═══╬═══╪═══╪═══╣
║ 2 │ 6 │ 3 ║ 4 │ 1 │ 5 ║ 9 │ 8 │ 7 ║
╟───┼───┼───╫───┼───┼───╫───┼───┼───╢
║ 9 │ 7 │ 4 ║ 8 │ 6 │ 3 ║ 1 │ 2 │ 5 ║
╟───┼───┼───╫───┼───┼───╫───┼───┼───╢
║ 8 │ 5 │ 1 ║ 7 │ 9 │ 2 ║ 6 │ 4 │ 3 ║
╠═══╪═══╪═══╬═══╪═══╪═══╬═══╪═══╪═══╣
║ 1 │ 3 │ 8 ║ 9 │ 4 │ 7 ║ 2 │ 5 │ 6 ║
╟───┼───┼───╫───┼───┼───╫───┼───┼───╢
║ 6 │ 9 │ 2 ║ 3 │ 5 │ 1 ║ 8 │ 7 │ 4 ║
╟───┼───┼───╫───┼───┼───╫───┼───┼───╢
║ 7 │ 4 │ 5 ║ 2 │ 8 │ 6 ║ 3 │ 1 │ 9 ║
╚═══╧═══╧═══╩═══╧═══╧═══╩═══╧═══╧═══╝
```

### The `display` module

The `display` module relies on the `matplotlib` library. You have to install it first to use this module.

To use use the module, add to the top of the program.

```python
import display
```

`puzzleDisp` inputs a 2D list of the puzzle and displays the puzzle.

```python
display.puzzleDisp(grid=grid)
```

`solDisp` inputs 2D lists of puzzle and solution and displays solution.

```python
display.solDisp(grid=grid, sol=sol)
```

`dispAll` displays both the puzzle and the solution.

```python
display.dispAll(grid=grid, sol=sol)
```
### The `collectdata` module

To use, import the module

```python
import collectdata
```
`collectBacktracking`, `collectConstraintPropagation`, `collectSimulatedAnnealing` collect runtime for the backtracking, constraint propagation and simulated annealing algorithm respectively. 

All functions input a string, which is a name a data file in the `dataset` folder.

The collected data is written in a `.csv` file in the `collected_data` folder.

## References

+ https://github.com/MaximeDaigle/sudoku
+ https://norvig.com/sudoku.html
+ https://www.sudocue.net/features.php
+ https://www.kaggle.com/code/lyly123/solve-sudoku-with-cnn-acc-97


