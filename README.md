# TIC-TAC-TOE-
Tic Tac Toe  Welcome to the classic game of Tic Tac Toe, implemented in c language . This repository hosts a simple yet engaging rendition of the timeless two-player game.
<br>
Author - Mubashira Awan
#include <stdio.h>
#include <stdbool.h>

// Function to initialize the game board
void initialize(char board[3][3]) {
    int i, j;
    for (i = 0; i < 3; i++) {
        for (j = 0; j < 3; j++) {
            board[i][j] = ' ';
        }
    }
}

// Function to print the game board
void print_board(char board[3][3]) {
    int i, j;
    printf("\n");
    for (i = 0; i < 3; i++) {
        for (j = 0; j < 3; j++) {
            printf(" %c ", board[i][j]);
            if (j < 2)
                printf("|");
        }
        printf("\n");
        if (i < 2)
            printf("---+---+---\n");
    }
    printf("\n");
}

// Function to check if the game is over (win or draw)
bool is_game_over(char board[3][3]) {
    int i, j;

    // Check rows and columns
    for (i = 0; i < 3; i++) {
        if (board[i][0] != ' ' && board[i][0] == board[i][1] && board[i][1] == board[i][2])
            return true; // Row win
        if (board[0][i] != ' ' && board[0][i] == board[1][i] && board[1][i] == board[2][i])
            return true; // Column win
    }

    // Check diagonals
    if (board[0][0] != ' ' && board[0][0] == board[1][1] && board[1][1] == board[2][2])
        return true; // Diagonal win
    if (board[0][2] != ' ' && board[0][2] == board[1][1] && board[1][1] == board[2][0])
        return true; // Diagonal win

    // Check for draw
    for (i = 0; i < 3; i++) {
        for (j = 0; j < 3; j++) {
            if (board[i][j] == ' ')
                return false; // Game is not over yet
        }
    }
    return true; // Draw
}

// Function to get player's move
void get_player_move(char board[3][3], int* row, int* col) {
    printf("Enter row and column (1-3): ");
    scanf("%d %d", row, col);
    (*row)--;
    (*col)--;
    while (board[*row][*col] != ' ' || *row < 0 || *row > 2 || *col < 0 || *col > 2) {
        printf("Invalid move. Enter row and column again (1-3): ");
        scanf("%d %d", row, col);
        (*row)--;
        (*col)--;
    }
}

// Function to perform player's move
void perform_player_move(char board[3][3], int row, int col) {
    board[row][col] = 'X';
}

// Function to perform computer's move
void perform_computer_move(char board[3][3]) {
    int row, col;
    do {
        row = rand() % 3;
        col = rand() % 3;
    } while (board[row][col] != ' ');
    board[row][col] = 'O';
}

int main() {
    char board[3][3];
    int row, col;

    initialize(board);
    print_board(board);

    while (!is_game_over(board)) {
        // Player's move
        get_player_move(board, &row, &col);
        perform_player_move(board, row, col);
        print_board(board);
        if (is_game_over(board)) {
            printf("Player wins!\n");
            break;
        }

        // Computer's move
        perform_computer_move(board);
        print_board(board);
        if (is_game_over(board)) {
            printf("Computer wins!\n");
            break;
        }
    }

    if (is_game_over(board) && !is_draw(board)) {
        printf("It's a draw!\n");
    }

    return 0;
}
