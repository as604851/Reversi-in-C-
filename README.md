# Reversi Game in C++

## Overview
This C++ program implements a basic version of the board game **Reversi** (also known as **Othello**). The game consists of two players who alternate placing their pieces on the board, trying to flip the opponent's pieces according to the rules of the game.

## Features
- Two-player game with alternating turns (Player 'x' and Player 'o').
- Board size is 9x9 (including borders).
- Players can flip opponent's pieces according to Reversi's rules.
- The game ends when no valid moves are left for both players.
- The board is displayed after each turn.

## Code Breakdown

### 1. **Including Headers**

```cpp
#include <iostream>
```

- This line includes the standard I/O stream library which allows us to print messages to the console and receive user input.

### 2. **Global Constants and Variables**

```cpp
const int SIZE = 9;
```

- This constant defines the board size. The board is 9x9 (including the extra border row and column, which are used for easier indexing).

### 3. **Function: `printBoard`**

```cpp
void printBoard(char board[10][10]) {
    std::cout << " "; 
    for (int i = 1; i < 9; i++) { 
        std::cout << " " << i; 
    } 
    std::cout << std::endl;
    for (int i = 1; i < 9; i++) {
        std::cout << i << " ";
        for (int j = 1; j < 9; j++) {
            std::cout << board[i][j] << " ";
        }
        std::cout << std::endl;
    }
}
```

- This function prints the current state of the Reversi board on the console.
    - The first loop prints the column numbers (1 through 8).
    - The second loop prints each row of the board, showing the content of each cell (either 'o', 'x', or space `' '`).
    - The board is printed from the second row and column to avoid printing the border.

### 4. **Function: `main`**

The `main` function is where most of the logic takes place.

```cpp
char f[10][10] = {
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '},
    {' ', ' ', ' ', ' ', 'x', 'o', ' ', ' ', ' ', ' '},
    {' ', ' ', ' ', ' ', 'o', 'x', ' ', ' ', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '}
};
```

- The board `f` is initialized as a 10x10 grid (with rows and columns numbered from 1 to 8). The inner rows and columns (from 1 to 8) represent the playable area.
- Initially, the board is set up with two pieces for each player (player 'o' and player 'x') in the middle. The center four squares are arranged as:
    - `f[5][5] = 'o'` (Player 'o')
    - `f[5][4] = 'x'` (Player 'x')
    - `f[4][5] = 'x'` (Player 'x')
    - `f[4][4] = 'o'` (Player 'o')

```cpp
char g[10][10] = {
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '}
};
```

- The array `g` is a copy of the initial board `f`. It is used to store a snapshot of the board that remains unchanged while the game is running (for comparison and backup purposes).

### 5. **Game Loop and Logic**

```cpp
while (1) {
    if (am % 2) {
        ch = 'x';  ch1 = 'x'; ch2 = 'o'; am++;  std::cout << "Spieler" << ch;
    }
    else {
        ch = 'o'; ch1 = 'o'; ch2 = 'x'; am++; std::cout << "Spieler" << ch;
    }
```
- The game alternates turns between two players. This loop runs infinitely (`while(1)`) until the game ends.
- The variable `am` keeps track of the turn number. If it's odd, player 'x' plays; if it's even, player 'o' plays.
- The `ch` variable determines which player is currently playing.

```cpp
for (int y = 0; y < 10; y++) {
    for (int x = 0; x < 10; x++) {
        g[y][x] = f[y][x];
    }
}
```
- The board `f` is copied to `g`, preserving the current game state for later comparison.

### 6. **Move Validation**

This section handles the core logic of validating a move. A valid move occurs when the player can "flip" the opponent's pieces according to the game rules (horizontal, vertical, or diagonal). The loop checks all 8 directions (right, left, down, up, and the four diagonals).

Example:
```cpp
if (f[y][x] == ch1 && f[y][x + 1] == ch2) {
    std::cout << "Prüfung rechts" << ' ' << y << x << ' ' << ch1 << ' ' << ch2 << std::endl;
    b++;
    while (f[y][b] == ch2) {
        b++;
        if (f[y][b] == ch1) { 
            e = 0; sp1 = 1; std::cout << "Prüfung rechts bestanden" << ' ' << y << x << ' ' << ch1 << ' ' << ch2 << std::endl;  
            goto stop18; 
        }
        if (f[y][b] == ' ') { e = 0; }
        if (f[y][b] == ch2) { e = 0; }
    }
```
- This code checks if there are opponent pieces (`ch2`) to the right of the current position (`f[y][x + 1]`). If the player can "capture" those pieces by placing a piece next to them, the pieces in between are flipped.

### 7. **Ending the Game**

```cpp
if (ende == 1) {
    for (int y = 0; y < 10; y++) {
        for (int x = 0; x < 10; x++) {
            f[y][x] = g[y][x];
        }
    }
```
- This part of the code checks if the game is over (`ende == 1`). If there are no more valid moves, the program resets the board and counts the points for each player, determining who won or if it was a draw.

## Conclusion
This program is a simplified implementation of **Reversi (Othello)** in C++. It handles basic gameplay with alternating turns, validates moves, and flips pieces according to the rules. However, it could benefit from further refinements like improving the game-ending logic and simplifying the move validation process.
