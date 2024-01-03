# AICP WEEK 5 TASK 5
# TIC TAC TOE 
#include <iostream>
#include <vector>
using namespace std;

void printBoard(const vector<vector<char>>& board);
bool makeMove(vector<vector<char>>& board, int row, int col, char player);
bool checkWin(const vector<vector<char>>& board, char player);
bool isBoardFull(const vector<vector<char>>& board);

int main() 
{
    const int BOARD_SIZE = 3;
    vector<vector<char>> board(BOARD_SIZE, vector<char>(BOARD_SIZE, ' '));

    int row, col;
    char currentPlayer = 'X';

    while (true) 
	{
        printBoard(board);

        cout << "Player " << currentPlayer << ", enter your move (row and column): ";
        cin >> row >> col;

        if (row < 0 || row >= BOARD_SIZE || col < 0 || col >= BOARD_SIZE || board[row][col] != ' ') 
		{
            cout << "Invalid move. Try again." << endl;
            continue;
        }

        if (makeMove(board, row, col, currentPlayer)) 
		{
       
            if (checkWin(board, currentPlayer)) 
			{
                printBoard(board);
                cout << "Player " << currentPlayer << " wins!" << endl;
                break;
            }

            
            if (isBoardFull(board)) 
			{
                printBoard(board);
                cout << "It's a tie!" << endl;
                break;
            }

            currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
        }
    }

    return 0;
}

void printBoard(const vector<vector<char>>& board) 
{
    cout << "  0 1 2" << endl;
    for (int i = 0; i < board.size(); ++i) 
	{
        cout << i << " ";
        for (int j = 0; j < board[i].size(); ++j) 
		{
            cout << board[i][j];
            if (j < board[i].size() - 1) 
			{
                cout << "|";
            }
        }
        cout << endl;
        if (i < board.size() - 1) 
		{
            cout << "  -----" << endl;
        }
    }
    cout << endl;
}

bool makeMove(vector<vector<char>>& board, int row, int col, char player) 
{
    if (board[row][col] == ' ') 
	{
        board[row][col] = player;
        return true;
    } else {
        return false;
    }
}

bool checkWin(const vector<vector<char>>& board, char player) 
{
  
    for (int i = 0; i < 3; ++i) 
	{
        if ((board[i][0] == player && board[i][1] == player && board[i][2] == player) ||
            (board[0][i] == player && board[1][i] == player && board[2][i] == player)) 
		{
            return true;
        }
    }

    if ((board[0][0] == player && board[1][1] == player && board[2][2] == player) ||
        (board[0][2] == player && board[1][1] == player && board[2][0] == player)) 
	{
        return true;
    }

    return false;
}

bool isBoardFull(const vector<vector<char>>& board) 
{
    for (int i = 0; i < board.size(); ++i) 
	{
        for (int j = 0; j < board[i].size(); ++j) 
		{
            if (board[i][j] == ' ') 
			{
                return false;
            }
        }
    }
    return true;
}
