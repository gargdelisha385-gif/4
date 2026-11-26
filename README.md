# 4
#include <stdio.h>

int main()
{
    char board[3][3] = {
        {' ', ' ', ' '},
        {' ', ' ', ' '},
        {' ', ' ', ' '}
    };

    int i, j;
    int row, col;
    int player = 1;
    int gameOver = 0;
    int moves = 0;
    char symbol;

    while(gameOver == 0)
    {
        // Display board
        printf("\nTIC TAC TOE\n");

        for(i = 0; i < 3; i++)
        {
            for(j = 0; j < 3; j++)
            {
                printf(" %c ", board[i][j]);

                if(j < 2)
                    printf("|");
            }

            printf("\n");

            if(i < 2)
                printf("---|---|---\n");
        }

        // Player turn
        printf("\nPlayer %d's turn\n", player);

        printf("Enter row (1-3): ");
        scanf("%d", &row);

        printf("Enter column (1-3): ");
        scanf("%d", &col);

        row--;
        col--;

        // Check valid position
        if(row < 0 || row > 2 || col < 0 || col > 2)
        {
            printf("Invalid position! Try again.\n");
            continue;
        }

        // Check empty position
        if(board[row][col] != ' ')
        {
            printf("Position already occupied! Try again.\n");
            continue;
        }

        // Place symbol
        if(player == 1)
        {
            symbol = 'X';
        }
        else
        {
            symbol = 'O';
        }

        board[row][col] = symbol;
        moves++;

        // Check horizontal and vertical wins
        for(i = 0; i < 3; i++)
        {
            if(board[i][0] == board[i][1] &&
               board[i][1] == board[i][2] &&
               board[i][0] != ' ')
            {
                gameOver = 1;
            }

            if(board[0][i] == board[1][i] &&
               board[1][i] == board[2][i] &&
               board[0][i] != ' ')
            {
                gameOver = 1;
            }
        }

        // Check diagonal wins
        if(board[0][0] == board[1][1] &&
           board[1][1] == board[2][2] &&
           board[0][0] != ' ')
        {
            gameOver = 1;
        }

        if(board[0][2] == board[1][1] &&
           board[1][1] == board[2][0] &&
           board[0][2] != ' ')
        {
            gameOver = 1;
        }

        // Announce winner
        if(gameOver == 1)
        {
            printf("\nPlayer %d wins!\n", player);
            break;
        }

        // Check draw
        if(moves == 9)
        {
            printf("\nGame is a draw!\n");
            gameOver = 1;
            break;
        }

        // Switch player
        if(player == 1)
        {
            player = 2;
        }
        else
        {
            player = 1;
        }
    }

    // Display final board
    printf("\nFinal Board:\n");

    for(i = 0; i < 3; i++)
    {
        for(j = 0; j < 3; j++)
        {
            printf(" %c ", board[i][j]);

            if(j < 2)
                printf("|");
        }

        printf("\n");

        if(i < 2)
            printf("---|---|---\n");
    }

    return 0;
}up