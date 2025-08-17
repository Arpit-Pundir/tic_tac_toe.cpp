# tic_tac_toe.cpp
Simple console based tic tac toe game that allows two players to play against each other
#include <iostream>
using namespace std;

char board[3][3];

void resetBoard() {
    char start = '1';
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            board[i][j] = start++;
        }
    }
}

void displayBoard() {
    cout << "\n";
    for (int i = 0; i < 3; i++) {
        cout << " ";
        for (int j = 0; j < 3; j++) {
            cout << board[i][j];
            if (j < 2) cout << " | ";
        }
        cout << "\n";
        if (i < 2) cout << "---+---+---\n";
    }
    cout << "\n";
}

bool checkWin(char player) {
    for (int i = 0; i < 3; i++) {
        if ((board[i][0] == player && board[i][1] == player && board[i][2] == player) ||
            (board[0][i] == player && board[1][i] == player && board[2][i] == player))
            return true;
    }
    if ((board[0][0] == player && board[1][1] == player && board[2][2] == player) ||
        (board[0][2] == player && board[1][1] == player && board[2][0] == player))
        return true;
    return false;
}

bool checkDraw() {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (board[i][j] != 'X' && board[i][j] != 'O')
                return false;
        }
    }
    return true;
}

bool makeMove(int choice, char player) {
    int row = (choice - 1) / 3;
    int col = (choice - 1) % 3;
    if (choice < 1 || choice > 9 || board[row][col] == 'X' || board[row][col] == 'O') {
        cout << "Invalid move! Try again.\n";
        return false;
    }
    board[row][col] = player;
    return true;
}

int main() {
    char currentPlayer = 'X';
    bool playAgain = true;
    int choice;

    while (playAgain) {
        resetBoard();
        bool gameOver = false;

        cout << "Welcome to Tic-Tac-Toe!\n";
        displayBoard();

        while (!gameOver) {
            cout << "Player " << currentPlayer << ", enter your move (1-9): ";
            cin >> choice;

            if (makeMove(choice, currentPlayer)) {
                displayBoard();

                if (checkWin(currentPlayer)) {
                    cout << "🎉 Player " << currentPlayer << " wins!\n";
                    gameOver = true;
                } else if (checkDraw()) {
                    cout << "It's a draw! 🤝\n";
                    gameOver = true;
                } else {
                    currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
                }
            }
        }

        char again;
        cout << "Do you want to play again? (y/n): ";
        cin >> again;
        if (again == 'n' || again == 'N') {
            playAgain = false;
            cout << "Thanks for playing!\n";
        }
    }
    return 0;
}
