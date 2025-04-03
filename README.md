# Reversi Board Simulation

## Overview
This project implements a simple simulation of a **Reversi-style board game** using **C++**. Reversi, also known as Othello, is a strategy board game where players take turns placing pieces on a grid, with the goal of capturing opponent pieces by surrounding them.

The program initializes a **9x9** board with predefined pieces and simulates a turn-based game, where the board state is updated continuously. The board state is displayed at each step, providing a dynamic, real-time simulation of the game’s evolution. This project primarily aims to showcase **C++** techniques such as board manipulation, game logic, and console output handling.

Although the game follows a simplified version of Reversi rules and is not fully interactive, it serves as a good foundation for building a more complete game.

## Features
- **Board Initialization**:
  - The board starts with predefined positions of player (`'o'`) and opponent (`'x'`) pieces.
  - The initial configuration mimics a typical Reversi setup, with pieces placed in a balanced, starting position.
  
- **Game Logic**:
  - The game operates in a loop, continuously checking each cell’s neighbors to determine whether pieces should be added, removed, or remain based on predefined conditions.
  - Pieces are placed in empty cells following specific rules based on the surrounding pieces:
    - **Survival**: A piece remains in its current position if it is surrounded by 2 or 3 other pieces.
    - **Overcrowding**: A piece is removed if it is surrounded by more than 3 pieces.
    - **Reproduction**: A new piece may be created in an empty cell if it has exactly 3 neighboring pieces.

- **Real-time Board Display**:
  - The board state is cleared and updated on each iteration using `system("CLS")` to refresh the screen.
  - The board is displayed using the `printBoard()` function, where each cell's state is printed in a grid format.

- **Keyboard Interaction**:
  - The game includes basic keyboard input handling with the **up arrow key (↑)** allowing the player to trigger specific actions during the simulation.

- **Continuous Game Loop**:
  - The game operates within an infinite loop, allowing the simulation to run indefinitely unless terminated by the user.

## Installation & Usage

### Prerequisites
- **Operating System**: Windows (since the program relies on Windows-specific headers such as `conio.h` and `windows.h`).
- **C++ Compiler**: A C++ compiler supporting C++11 or later, such as **MinGW/g++** or **MSVC** (Microsoft Visual Studio C++ compiler).

### Steps to Compile and Run

1. **Clone the Repository**:
   ```sh
   git clone https://github.com/your-username/reversi-simulation.git
   cd reversi-simulation
   ```

2. **Compile the Program**:
   ```sh
   g++ -o reversi reversi.cpp -std=c++11
   ```

3. **Run the Executable**:
   ```sh
   ./reversi
   ```

## Code Explanation

### 1. Board Initialization
The program initializes two 9x9 arrays (`f` and `g`) representing the game board at different stages:

```cpp
char f[9][9] = {
    {' ', 'o', ' ', ' ', ' ', ' ', 'o', ' ', ' '},
    {' ', 'o', ' ', ' ', ' ', ' ', 'o', ' ', ' '},
    {' ', 'o', ' ', ' ', ' ', ' ', 'o', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '},
    {' ', ' ', 'o', 'o', ' ', ' ', 'o', ' ', ' '},
    {' ', ' ', ' ', 'o', ' ', ' ', 'o', ' ', ' '},
    {' ', ' ', ' ', 'o', ' ', ' ', 'o', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '}
};
```
`f` represents the initial board configuration with `'o'` and `'x'` placed at specific locations.

`g` is an empty board (initialized with `' '`), which will later be populated during the game logic.

### 2. Print Board Function
The `printBoard()` function is used to display the board state on the console:

```cpp
void printBoard(char board[9][9]) {
    for (int i = 0; i < 9; i++) {
        for (int j = 0; j < 9; j++) {
            std::cout << board[i][j] << " ";
        }
        std::cout << std::endl;
    }
}
```
It iterates through each row and column to print the current board state in a grid format.

### 3. Game Loop and Logic
The main loop continuously updates the board:

```cpp
int main() {
    int zu = 0;
    char f[9][9], g[9][9];  
    int b = 0;
    int a = 0;
    int ki1 = 1;
start:
    if (_kbhit()) ki1 = _getch();

    if (ki1 == 72) {  // Up arrow key pressed
        f[4][4] = 'o';
        f[2][4] = 'o';
        f[3][4] = 'o';
        f[4][1] = 'o';
        f[2][1] = 'o';
        f[3][1] = 'o';
        ki1 = 0;
    }
```
This section handles keyboard input and updates the board when the up arrow key is pressed.

### 4. Checking Surrounding Cells
For each cell, the program evaluates its neighbors:

```cpp
for (int y = 0; y < 9; y++) {
    for (int x = 0; x < 9; x++) {
        if (f[y][x] == 'o') { a++; }
        if (f[y][x + 1] == 'o') { b++; }
        if (f[y][x - 1] == 'o') { b++; }
        if (f[y + 1][x] == 'o') { b++; }
        if (f[y - 1][x] == 'o') { b++; }
    }
}
```
This determines whether a piece remains, is removed, or a new piece is placed.

### 5. Clearing and Updating the Board
```cpp
Sleep(100);
system("CLS");
printBoard(g);
```
This refreshes the board after each iteration.

### 6. Infinite Loop
```cpp
goto start;
return 0;
```
The game loops back to the beginning, running indefinitely.

---

This project provides a foundation for developing a more advanced, interactive Reversi game with AI and enhanced rules.
