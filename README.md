#include <iostream>
#include <vector>

using namespace std;

// Function to print the Tic-Tac-Toe board
void printBoard(const vector<vector<char>>& board) {
    for (const auto& row : board) {
        for (char cell : row) {
            cout << cell << " | ";
        }
        cout << endl << "---------" << endl;
    }
}

// Function to check if the current player has won
bool checkWinner(const vector<vector<char>>& board, char player) {
    // Check rows and columns for a win
    for (int i = 0; i < 3; ++i) {
        if ((board[i][0] == player && board[i][1] == player && board[i][2] == player) ||
            (board[0][i] == player && board[1][i] == player && board[2][i] == player)) {
            return true;
        }
    }

    // Check diagonals for a win
    return (board[0][0] == player && board[1][1] == player && board[2][2] == player) ||
           (board[0][2] == player && board[1][1] == player && board[2][0] == player);
}

// Function to check if the board is full (a draw)
bool isBoardFull(const vector<vector<char>>& board) {
    for (const auto& row : board) {
        for (char cell : row) {
            if (cell == ' ') {
                return false;
            }
        }
    }
    return true;
}

int main() {
    // Initialize the game board
    vector<vector<char>> board(3, vector<char>(3, ' '));

    // Initialize players
    char players[] = {'X', 'O'};
    int currentPlayer = 0;

    while (true) {
        // Display the current state of the board
        printBoard(board);

        // Prompt the current player to enter their move
        int row, col;
        cout << "Player " << players[currentPlayer] << ", enter row (0, 1, or 2): ";
        cin >> row;
        cout << "Player " << players[currentPlayer] << ", enter column (0, 1, or 2): ";
        cin >> col;

        // Check if the chosen position is valid
        if (board[row][col] != ' ') {
            cout << "Invalid move. Try again." << endl;
            continue;
        }

        // Update the game board with the player's move
        board[row][col] = players[currentPlayer];

        // Check for a win
        if (checkWinner(board, players[currentPlayer])) {
            printBoard(board);
            cout << "Player " << players[currentPlayer] << " wins!" << endl;
            break;
        }

        // Check for a draw
        if (isBoardFull(board)) {
            printBoard(board);
            cout << "It's a draw!" << endl;
            break;
        }

        // Switch players for the next turn
        currentPlayer = 1 - currentPlayer;
    }

    return 0;
}
