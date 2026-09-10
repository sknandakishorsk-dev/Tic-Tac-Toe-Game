# Tic-Tac-Toe-Game
#include <iostream>
using namespace std;

// Function to display the game board
void displayBoard(char board[3][3])
{
    cout << "\n";
    cout << " " << board[0][0] << " | " << board[0][1] << " | " << board[0][2] << "\n";
    cout << "---|---|---\n";
    cout << " " << board[1][0] << " | " << board[1][1] << " | " << board[1][2] << "\n";
    cout << "---|---|---\n";
    cout << " " << board[2][0] << " | " << board[2][1] << " | " << board[2][2] << "\n";
    cout << "\n";
}

// Function to check whether a player has won
bool checkWin(char board[3][3], char player)
{
    // Check rows
    for (int i = 0; i < 3; i++)
    {
        if (board[i][0] == player &&
            board[i][1] == player &&
            board[i][2] == player)
        {
            return true;
        }
    }

    // Check columns
    for (int i = 0; i < 3; i++)
    {
        if (board[0][i] == player &&
            board[1][i] == player &&
            board[2][i] == player)
        {
            return true;
        }
    }

    // Check main diagonal
    if (board[0][0] == player &&
        board[1][1] == player &&
        board[2][2] == player)
    {
        return true;
    }

    // Check other diagonal
    if (board[0][2] == player &&
        board[1][1] == player &&
        board[2][0] == player)
    {
        return true;
    }

    return false;
}

int main()
{
    char board[3][3] = {
        {'1', '2', '3'},
        {'4', '5', '6'},
        {'7', '8', '9'}
    };

    char player = 'X';
    int choice;
    int moves = 0;

    cout << "============================\n";
    cout << "       TIC-TAC-TOE GAME\n";
    cout << "============================\n";

    while (true)
    {
        displayBoard(board);

        cout << "Player " << player << ", enter a position (1-9): ";
        cin >> choice;

        // Validate position
        if (choice < 1 || choice > 9)
        {
            cout << "Invalid position! Please enter 1 to 9.\n";
            continue;
        }

        int row = (choice - 1) / 3;
        int col = (choice - 1) % 3;

        // Check if position is already occupied
        if (board[row][col] == 'X' || board[row][col] == 'O')
        {
            cout << "Position already occupied! Choose another position.\n";
            continue;
        }

        // Place player's symbol
        board[row][col] = player;
        moves++;

        // Check for winner
        if (checkWin(board, player))
        {
            displayBoard(board);
            cout << "Congratulations! Player " << player << " wins!\n";
            break;
        }

        // Check for draw
        if (moves == 9)
        {
            displayBoard(board);
            cout << "Game Draw!\n";
            break;
        }

        // Switch player
        if (player == 'X')
            player = 'O';
        else
            player = 'X';
    }

    return 0;
}